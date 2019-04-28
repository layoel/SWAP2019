# TRABAJO FINAL: Creación de una granja web con docker.

Para realizar la instalación de Docker vamos a seguir el tutorial de [esta página](https://www.digitalocean.com/community/tutorials/como-instalar-y-usar-docker-en-ubuntu-16-04-es)

Instalaremos Docker en una máquina con Ubuntu 16.04 como sistema operativo.

Para emprezar necesitamos actualizar, para lo cual usaremos el comando:
```BASH
sudo apt-get update
```

Añadimos la clave GPG para el repositorio oficial de docker.
![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/1.JPG)

A continuación tenemos que agregar al repositorio de ubuntu lo siguiente, para poder instalar docker desde su repositorio oficial. Y actualizamos la base de datos de paquetes de ubuntu con los añadidos anteriormente.

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/2.JPG)

Comprobamos si tenemos alguna versión de Docker instalada en nuestro sistema. 

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/3.JPG)

Instalamos docker-engine con la siguiente instrucción.

```BASH
sudo apt-get install -y docker-engine
```

Una vez instalado, comprobamos el estado de docker y veremos que está activo y en ejecución.

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/4.JPG)

Tenemos dos opciones para ejecutar comandos docker. 
- Una es que cada vez que queramos ejecutar una instruccion docker tengamos que usar **sudo**, porque necesita privilegios de root.
- La otra es añadir el usuario con el que vamos a ejecutar instrucciones docker al grupo de usuarios docker usando:

```BASH
sudo usermod -aG docker $(whoami)
```
![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/12.JPG)

Ya tenemos instalado docker en nuestro equipo. Ahora si queremos ver información sobre Docker en el sistema podemos usar:

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/5.JPG)

Nosotros en este caso vamos a trabajar con **imágenes de Docker**.

Para crear nuestra granja web, necesitamos dos servidores con apache y uno con nginx. Por lo que vamos a buscar primero las **imágenes** que hay en docker con **apache** y despues las **imágenes** que hay con **nginx**.

Busco imagenes de apache en docker:

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/6.JPG)

Busco imagenes de nginx en docker:

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/7.JPG)

Creación de una máquina con nginx
![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/8.JPG)
A partir de la imagen oficial de nginx creamos el contenedor nginx1, que expone los puertos 80 y
443 del contenedor en los puertos 8080 y 8443 del host. Además el contenedor se inicia tras la
ejecución.

Comprobamos que podemos acceder al servidor NGINX en http://localhost:8080

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/9.JPG)
Para ver todos los contenedores que están ejecutándose:

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/10.JPG)

Para ver todos los contenedores:
![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/11.JPG)

Practica 3 cpd crear contenedores docker  ejemplo de nginx
practica 4 dockerfile crear 3 maquinas

https://blog.dinahosting.com/servicio-web-con-docker-y-docker-compose/