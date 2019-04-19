# Práctica 4: Asegurar la granja web

## Certificado SSL autofirmado (HTTPS)
Inicialmente tenemos que crear una nueva maquina virtual con ubuntu server que hará las funciones de balanceador, este equipo se llama LB la  IP de mi balanceador es 192.168.80.133 está en red con las maquinas m1 y m2

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/1.JPG)

En esta máquina no hemos hecho como en las anteriores en la instalación unicamente hemos marcado el servicio ssh y no hemos instalado LAMP para poder tener libre el puerto 80 que es el que se usará para el balanceo de carga.

Vamos a instalar *nginx* escribiendo en consola:
```bash
elvira@LB:~$ sudo apt-get install nginx
```
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/2.JPG)

Una vez instalado el servicio, lo iniciamos:
```bash
elvira@LB:~$ sudo systemctl start nginx
```
En el navegador podemos ver que el nginx está funcionando.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/4.JPG)

A continuación, configuraremos nginx para ello modificamos el fichero de configuración que está en */etc/nginx/conf.d/default.conf*
```bash
elvira@LB:~$ sudo nano /etc/nginx/conf.d/default.conf
```
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/3.JPG)

Al editar este fichero, hemos configurado nuestro balanceador de carga con el algoritmo por turnos *round-robin* para que los cambios se apliquen, reiniciamos el servicio con:
```bash
elvira@LB:~$ sudo service nginx restart
```



## Cortafuegos

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/9.JPG)
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/10.JPG)


## Certbot 

En este [enlace](https://certbot.eff.org/lets-encrypt/ubuntuxenial-nginx) Seleccionando nuestro balanceador y el sistema operativo sobre el que trabajamos, nos facilita una guia de instalación de certbot.

