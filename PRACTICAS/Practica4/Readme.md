# Práctica 4: Asegurar la granja web

## Certificado SSL autofirmado (HTTPS)

Para esta práctica usaré de nuevo los servidores web **m1**, **m2** y mi **LB** y añadiremos un nuevo servidor que será el que haga de **firewall**.

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

Tenemos que editar el archivo de configuración:
```bash
elvira@:~m1$ sudo nano /etc/apache2/sites-avaliable/default-ssl
```
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/3.JPG)

Reiniciamos el servicio apache y activamos el sitio default-ssl
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/4.JPG)

Ahora comprobamos que todo funciona correctamente haciendo peticiones por *HTTPS* al servidor.
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/5.JPG)










## Cortafuegos

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/9.JPG)
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/10.JPG)


## Certbot 

En este [enlace](https://certbot.eff.org/lets-encrypt/ubuntuxenial-nginx) Seleccionando nuestro balanceador y el sistema operativo sobre el que trabajamos, nos facilita una guia de instalación de certbot.

