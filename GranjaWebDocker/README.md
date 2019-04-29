# TRABAJO FINAL: Creación de una granja web con docker.

## ¿Qué es Docker?

Docker es una herramienta cuya finalidad es crear contenedores que sean ligeros y portables, para aplicaciones software que puedan ejecutarse en cualquier máquina que tenga instalado Docker, sin depender del sistema operativo anfitrión de esa máquina. Esto último facilita los despliegues enormemente.
- Ligeros porque son procesos que comparten el kernel del SO.
- Portables porque se pueden crear localmente y ejecutar en cualquier entorno no en computación en la nube. Además, al desplegarse en proveedores en la nube, sin tener que definir una infraestructura, se reducen los costes a dichos proveedores y estos a su vez ofrecen menor coste en la ejecución.
- Intercamiables porque se pueden desarrollar nuvas actualizaciones y son fácilmente actualizables.
- Escalables porque se pueden añadir y distribuir copias.
- Flexibles porque hay gran cantidad de aplicaciones que pueden ser incluidas en un contenedor.

### ¿Qué es un contenedor?

Un contenedor simplifica la virtualización clásica, porque es capaz de montar un sistema de ficheros completo con un sistema operativo completo, puede alojar cualquier librería que se pueda instalar y sobre todo, lo más importante es que podemos desplegar nuestra aplicación sin necesidad de tener un hypervisor.

### Beneficios de usar Docker

El uso de Docker beneficia tanto a desarrolladores, testers y administradores de sistemas.

- **Desarrolladores**: el uso de Docker hace que puedan centrarse en desarrollar su código sin preocuparse si dicho código funcionará en la máquina en la que se ejecutará al final.

- **Testers**: con Docker se pueen crear entornos de pruebas. Es sencillo crear y borrar un contenedor, además como dijimos anteriormente, son ligeros y podemos ejecutar varios contenedores en una misma máquina.

- **Sysadmin** (Administradores de sistemas): debido a la cualidad de que los contenedores son más ligeros que las máquinas virtuales, se reduce el número de máquinas necesarias para tener en un entorno.

### Comparativa Docker vs Virtual Machine

Son conceptos similares, pero un contenedor es más ligero. Una máquina virtual necesita instalar el Sistema Operativo para que funcione, mientras que Docker usa el Sistema Operatívo que tiene la máquina en la que se ejecuta el contenedor.

Los contenedores Docker se parecen a las máquinas virtuales porque encapsulan dentro del contenedor los recursos más básicos que no cambian de un ordenador a otro y los aspectos más específicos del sistema que pueden dar más problemas a la hora de llevar el software de un lado a otro.

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/13.png)

### Elementos básicos de Docker

- **Imágenes**: Es una plantilla que contiene el estado de un contenedor. Digamos que podría ser como un snapshot de una máquina virtual. Por ejemplo, nosotros usaremos para montar la granja web una imágen con ubuntu y apache y otra imagen con ubuntu y nginx. 
Las imágenes se usan para crear contenedores y no varían. El registro que tiene Docker donde podemos obtener las imágenes de base que necesitemos o crear nuestras propias imágenes y compartirlas, se llama [**dockerhub**](https://hub.docker.com/). Que funciona como una especie de repositorio de imágenes ya diseñadas.

- **Dockerfile**: es el archivo de configuración que se usa para crear imágenes. En este archivo indicamos que es lo que queremos que tenga la imagen y los comandos para instalar las herramientas que necesitamos. Un ejemplo de Dockerfile seria el siguiente:

```Bash
FROM debian
MAINTAINER Usuario elvira "usuario@ugr.es"
RUN apt-get update && apt-get install -y apache2 && apt-get clean && rm -rf /var/lib/apt/lists/*
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
EXPOSE 80
ADD ["index.html","/var/www/html/"]
ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

```
En la [documentación de docker](https://docs.docker.com/engine/reference/builder/) hay varios ejemplos y explicaciones detalladas de como escribir y crear nuestro propio dockerfile.


- **Contenedores**: Son instancias en ejecución,los que ejecutan nuestra aplicación. Es como si restauramos una máquina virtual a partir de un snapshot. Con una única imagen, podemos crear tantos contenedores como queramos. Así en nuestra granja web, podremos tener copias de nuestra aplicación web en varios contenedores, para despues a través del balanceador de carga, distribuir los accesos a la aplicación y ofrecer servicios con mejores grarantías y menos carga de peticiones por contenedor. También podemos crear distitnas versiones de contenedores, hacer commit para crear otra imagen con los cambios realizados y si algo va mal, volver a la versión anterior del contenedor.

- **Volúmenes**: Se usan para compartir datos entre contenedores. Los datos persistentes, deben guardarse en volúmenes de tal forma que cuando borremos un contenedor no perdamos los datos importantes.

### [Docker Machine, Docker compose y Docker Swarm.](https://blog.codeship.com/docker-machine-compose-and-swarm-how-they-work-together/)

El proyecto Docker engloba una serie de herramientas muy útiles. Podemos seleccionar la que mas se adapte a nuestro problema dependiendo del alcance que tengamos que cubrir. 

Por ejemplo si solo queremos probar una aplicación, usaremos *docker machine* para crear un contenedor y probarla. Si queremos probar el funcionamiento de un conjunto de aplicaciones relacionadas entre si usaremos *docker compose* y por último si queremos montar un sistema que sea redundante y que use balanceo entre máquinas usaremos *docker swarm*. 

A continuación explicaremos brevemente en que consiste cada una de las herramientas mencionadas anteriormente.

- **Docker Machine**: Esta herramienta nos ayuda a crear contenendores en plataformas de virtualización como: VMware, VirtualBox y en otras plataformas como AWS, Azure, DigitalOcean, Exoscale, Google Compute Engine, OpenStack, SpofLayer, VMware vSphere y vCloud Aire. Para instalar docker machine podemos seguir [este tutorial](https://docs.docker.com/machine/install-machine/), de la web oficial de docker.

- **Docker Compose**: Con esta herramienta podemos gestionar varios contenedores que funcionan en conjunto. Con Docker Compose podemos administrar los contenedores con un archivo de configuración que se llama *docker-compose.yml* donde determinaremos como estarán vinculados los contenedores, los puertos que deben estar expuestos al usuario final... 
En el siguiente archivo de ejemplo hemos creado un entorno de wordpress basado en una base de datos MySQL y el propio Wordpress.
Docker Compose nos permite crear soluciones más complejas que requieren de multiples aplicaciones.

```Bash
version: '3.3'

services:
 db:
 	image: mysql:5.7
 	volumes:
 	- db_data:/var/lib/mysql
 	restart: always
 	environment:
		 MYSQL_ROOT_PASSWORD: somewordpress
		 MYSQL_DATABASE: wordpress
		 MYSQL_USER: wordpress
		 MYSQL_PASSWORD: ECAwordpress
 wordpress:
	 depends_on:
	 - db
	 image: wordpress:latest
	 ports:
	 - "8000:80"
	 restart: always
	 environment:
		 WORDPRESS_DB_HOST: db:3306
		 WORDPRESS_DB_USER: wordpress
		 WORDPRESS_DB_PASSWORD: ECAwordpress
volumes:
 db_data
```

- **Docker Swarm**: Esta herramienta, nos permite distribuir contenedores entre distintas máquinas de forma que pueda distribuirse la ejecución. Esta característica hace que sea la herramienta mas interesante de las que dispone docker. Podemos crear agrupaciones de contenedores ya agrupados anteriormente, es decir, con esto podemos crear clusteres de contenedores con las aplicaciones que necesitemos. 

## Instalación de Docker

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

## Creando mi Granja Web

Primero instalaremos docker-machine. Yo voy a instarlo en windows por lo que pondré los pasos para hacerlo con mi sistema operativo, pero en la web de docker tenemos la[ documentación](https://docs.docker.com/machine/install-machine/) de como hacerlo si el sistema operativo anfitrión es linux o macos

Necesitamos tener instalado Git BASH en windows y virtualbox o bien VMware. Ejecutaremos en una terminal de Git Bash la siguiente instrucción.

```bash
$ base=https://github.com/docker/machine/releases/download/v0.16.0 &&
  mkdir -p "$HOME/bin" &&
  curl -L $base/docker-machine-Windows-x86_64.exe > "$HOME/bin/docker-machine.exe" &&
  chmod +x "$HOME/bin/docker-machine.exe"
```

Y comprobamos la versión que se ha instalado con el comando
```bash
$ docker-machine version
```
![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/15.JPG)

Creamos una máquina con Docker-machine

```bash
$ docker-machine create --virtualbox-boot2docker-url https://github.com/boot2docker/boot2docker/releases/download/v19.03.0-beta3/boot2docker.iso m1
```
La imágen que vamos a instalar en la maquina m1 que estamos creando es un linux con docker instalado.

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/16.JPG)

Para ver la lista de maquinas creadas con docker-machine usamos:

```bash
$ docker-machine ls
```
Como podemos observar en la imagen siguiente yo solo tengo un contenedor ejecutandose que se llama *m1* y su ip es la *192.168.99.101*

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/17.JPG)

Para saber la ip de la maquina creada podemos ejecutar el comando:

```bash
$ docker-machine ip m1
```

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/34.JPG)

Accedemos por ssh a la máquina *m1* que será el nodo principal de nuestra granja web.

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/21.JPG)

Vamos a usar docker swarm para crear un cluster con las 4 máquinas. Usaremos la siguiente instrucción.

```bash
docker@m1:~$ docker swarm init --advertise-addr 192.168.99.101
```
![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/20.JPG)

Esta instrucción indicará que es el nodo principal y si observamos la imagen anterior, tras ejecutarlo nos da un token que tendremos que usar en *m2* y *m3* y el resto de máquinas que queramos añadir.

Para comprobar cuantos nodos hay actualmente usamos:

```bash
docker@m1:~$ docker node ls
```

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/18.JPG)

Nos dirá el id del nodo el nombre, el estado, si esta activo o no, el estatus si es el principal o es secundario, además de la version de docker que se está usando.


Saldremos de la máquina m1 
```bash
docker@m1:~$ exit
logout

```

Y crearemos el nodo 2 que le vamos a llamar *m2*. Ahora ya tenemos descargada la imagen, por lo que con el siguiente comando se creará la maquina con la imagen que descargamos anteriormente de github.

```bash
$ docker-machine create m2
```

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/22.JPG)

Entramos por ssh al servidor *m2* para añadirlo a la granja web.

```bash
docker@m2:~$ docker swarm join --token SWMTKN-1-3blnb40782us5dh71swqb9j633ueozsqn5pstu4j5vb9vznrz0-3imvy2pcvd0aiqf1b2jjjx7j8 192.168.99.101:2377
This node joined a swarm as a worker.
```

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/23.JPG)

Si entramos por ssh en el nodo *m1* podemos ver que *m2* ya esta añadido.

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/24.JPG)

Estos últimos pasos los realizamos también para *m3* y *m4*

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/25.JPG)
![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/26.JPG)

Entramos de nuevo en el nodo *m1* y vemos que ya están todos los nodos añadidos como si fuera un único nodo, sabiendo por el * que aparece junto a su identificador y por el estatus que el principal es **m1**

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/27.JPG)

Una vez tenemos todos los nodos activos y añadidos al cluster, vamos a lanzar un servicio web con 4 replicas que se distribuyen entre los 4 nodos que hemos creado.

```bash
docker@m1:~$ docker service create --name web --replicas 4 --mount type=bind,src=/etc/hostname,dst=/usr/share/nginx/html/index.html,readonly --publish published=8080,target=80 nginx
```

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/28.JPG)

Si ejecutamos el comando curl desde por ejemplo el nodo m1, veremos que cada vez responde un servidor a la petición web.

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/29.JPG)

Podemos comprobar que el servicio ha lanzado 4 contenedores, uno en cada nodo.

```bash
docker@m1:~$ docker service ps web
```

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/30.JPG)

Podemos reducir o ampliar el número de nodos para escalar nuestra granja web con:

```bash
docker@m1:~$ docker service scale web=2
```

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/31.JPG)

Esto hace que nuestra granja web sea escalable. Podemos tener varias máquinas configuradas y añadidas a la granja y que el sistema funcione con 2 nodos únicamente y en los momentos en los que se prevea un incremento en el número de peticiones podemos escalar hasta 4 el número de nodos con la arquitectura que tenemos montada en este momento.

Para comprobar la alta disponibilidad de la granja web vamos a parar uno de los nodos simulando que está en mantenimiento por algún motivo, o incluso que tiene algún problema de hardware y se ha apagado.

```bash
$  docker-machine stop m3
```

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/32.JPG)

Comprobamos de nuevo con curl que la granja web sigue funcionando y que no ha visto interrumpida su disponibilidad debido a que el nodo m3 no esté funcionando.

![imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/33.JPG)
