# Práctica 4: Asegurar la granja web

## Certificado SSL autofirmado (HTTPS)

Para esta práctica usaré de nuevo los servidores web **m1** (192.168.80.131), **m2** (192.168.80.132) y mi **LB** (192.168.80.133).

Comenzamos trabajando sobre **m1**, esta máquina tiene la ip **192.168.80.131** y tiene apache instalado. Sobre él vamos a instalar un certificado autofirmado para poder configurar el acceso por *HTTPS*.

Para generar el certificado ejecutamos la siguiente orden en la consola:

```bash
elvira@m1:~$ sudo a2enmod ssl
```

Reiniciamos el servicio de apache

```bash
elvira@:~m1$ sudo service apache2 restart
```

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/1.JPG)

Creamos una carpeta para guardar el certificado ssl  y lo generamos con **openssl**

```bash
elvira@m1:~$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
```

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/2.JPG)

Tenemos que editar el archivo de configuración añadiendo las dos líneas que tenemos marcadas en amarillo en la imagen siguiente:

```bash
elvira@:~m1$ sudo nano /etc/apache2/sites-avaliable/default-ssl
```

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/3.JPG)

Reiniciamos el servicio apache y activamos el sitio default-ssl

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/4.JPG)

Ahora comprobamos que todo funciona correctamente haciendo peticiones por *HTTPS* al servidor.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/5.JPG)

Para configurar el servidor web **m2** copiaremos los certificados generados en **m1** a **m2**, yo he usado rsync pero tambien se puede hacer con scp.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/7.JPG)

igualmente tenemos que editar el fichero default-ssl y reiniciar el servicio y recargar apache2.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/6.JPG)

también tenemos que copiar los certificados al balanceador, para eso crearemos una carpeta y ejecutaremos el comando rsync

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/8.JPG)

Editamos el fichero de configuración de nginx añadiendo los certificados que hemos copiado y que escuche en el puerto 443 ssl.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/9.JPG)

Reiniciamos el servicio
```bash
elvira@:~m1$ sudo service nginx restart
```
Ahora probamos que el balanceador con nginx sirve las web con https usando curl:

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/10.JPG)

## Cortafuegos

Vamos a configurar iptables en el servidor **m1** con la ip 192.168.80.131. La información sobre el uso de iptables la podemos encontrar en el **man iptables** o bien ejecutando:
```bash
elvira@:~m1$ iptables -h
```
Comenzaremos comprobando el estado del cortafuegos.
```bash
elvira@:~m1$ sudo iptables -L -n -v 
```
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/11.JPG)

Como aún no tengo definida ninguna regla en mi cortafuegos, vemos que acepta todo el tráfico. Ahora vamos a empezar con la configuración, primero **bloqueando todo el tráfico**.

```bash
elvira@:~m1$ sudo iptables -P INPUT DROP 
elvira@:~m1$ sudo iptables -P OUTPUT DROP
elvira@:~m1$ sudo iptables -P FORWARD DROP
```
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/12.JPG)

Para aceptar todo y volver a la politica por defecto de aceptar todo añadimos las siguientes reglas de iptables:
```bash
elvira@:~m1$ iptables -F
elvira@:~m1$ iptables -X
elvira@:~m1$ iptables -Z
elvira@:~m1$ iptables -t nat -F
elvira@:~m1$ iptables −P INPUT ACCEPT
elvira@:~m1$ iptables −P OUTPUT ACCEPT
elvira@:~m1$ iptables −P FORWARD ACCEPT
```
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/13.JPG)

Si solo queremos **bloquear el tráfico de entrada** añadiremos las siguientes ordenes a iptables.

```bash
elvira@:~m1$ sudo iptables -P INPUT DROP 
elvira@:~m1$ sudo iptables -P FORWARD DROP
elvira@:~m1$ sudo iptables -P OUTPUT ACCEPT
elvira@:~m1$ sudo iptables -A -m state --state NEW, ESTABLISHED -j ACCEPT
```
En [esta web](http://www.seavtec.com/en/content/soporte/documentacion/iptables-howto-ejemplos-de-iptables-para-sysadmins) tenemos unos cuantos ejemplos para sysadmins de como configurar iptables.

Creamos un script con todas las reglas que necesitamos para proteger nuestro servidor. Inicialmente vamos a bloquear cualquier tipo de trafico, a continuación permitiremos cualquier acceso desde la interfaz lo, y como nuestro equipo es un servidor web, vamos a permitir el acceso al puerto 80 y al 443 y por último permitimos acceso ssh al servidor solo desde la ip 192.168.80.132.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/15.JPG)

Ejecución script iptables en m1
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/14.JPG)

Comprobamos que podemos conectar por SSH solo desde la ip que indicamos.
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/16.JPG)

Y también comprobamos que podemos acceder a la web por el puerto 80 y el 443
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/17.JPG)

Ahora lo añadimos para que se ejecute al inicio cuando encendamos el equipo. Se puede hacer de dos formas, una añadiendolo en el fichero **crontab** con la directiva **@reboot /home/elvira/reglas_cortafuegos.sh** o bien aladiendolo al fichero **/etc/rc.local**

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/18.JPG)

## Certbot 

En este [enlace](https://certbot.eff.org/lets-encrypt/ubuntuxenial-nginx) Seleccionando nuestro balanceador y el sistema operativo sobre el que trabajamos, nos facilita una guia de instalación de certbot. Pero no tengo un dominio para poder hacer este ejercicio opcional.

