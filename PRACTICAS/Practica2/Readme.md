# Práctica 2: Clonar la información de un sitio web

Como aproximación inicial para clonar la información de un sitio web pensamos en copiar archivos por ssh. Veamos un ejemplo de como se hace:

He copiado el archivo **archivo** de *m1* a *m2*. Para copiar archivos podemos usar el comando **ssh 192.168.80.132 'cat > ~/archivo** pero si queremos copiar carpetas completas tendremos que comprimirlas, y copiarlas via ssh de *m1* a *m2*, lo comprimimos con tar y redireccionamos con ssh para la copia.

*elvira@m1:~$ **tar czf - /var/www/* |ssh 192.168.80.132 'cat > ~/tar.tgz***

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica2/imagenes/1.JPG)

Para copiar archivos o carpetas de un equipo a otro de forma puntual, está bien el comando anterior pero si queremos que se haga de forma automática por ejemplo para hacer copias de seguridad o para sincronizar información entre servidores usaremos **rsync**. Si no lo tenemos instalado podemos hacerlo con la siguiente orden:

*elvira@m2:~$ **sudo apt-get install rsync***
Primero cambiamos el dueño de los directorios /var/www en m1 para que sea el mismo user que accede desde m2 y no haya problemas de permisos
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica2/imagenes/2.JPG) //

En la siguiente imagen usamos rsync para copiar archivos de m1 a m2 via ssh.

*elvira@m2:~$ **rsync -avz -e ssh 192.168.80.131:/var/www/ /var/www/***

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica2/imagenes/3.JPG) 

Pero esta tarea se puede automatizar en lugar de tener que ejecutar cada cierto tiempo el comando anterior, pero primero necesitamos que nuestros servidores "confien el uno en el otro" y no pida la contraseña cada vez que queramos conectar por ssh.

Si creamos una clave pública y privada y usamos ese par de claves para el acceso, ya no necesitaremos introducir más la contraseña desde el equipo o dispositivo donde tengamos la pareja de claves. 
Para generar las claves hemos usado los siguientes comandos:
*elvira@m2:~$**ssh-keygen -b 4096 -t rsa***
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica2/imagenes/4.JPG) 

Una vez creadas el par de claves copiamos la clave publica al equipo *m1* con el comando: 
*elvira@m2:~$**ssh-copy-id 192.168.80.131***
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica2/imagenes/5.JPG) 

Ahora probamos a crear una copia del directorio */var/www/* de *m1* a *m2* ya que m1 es nuestro servidor en producción y estará atendiendo peticiones de los equipos que soliciten la web, nos conectaremos por ssh desde m2 y realizaremos la copia de la carpeta anterior de m1 a m2 para que tenga el contenido actualizado.[Aquí](https://kb.iweb.com/hc/es/articles/230241568-Copiar-un-archivo-hacia-otro-servidor-v%C3%ADa-SSH) tenemos información de como realizar copias o mover ficheros o archivos con ssh. Y vemos que ya no hay que introducir la clave para conectarte por ssh.

*elvira@m2:~$** ssh 192.168.80.131 rsync -avz -e ssh /var/www/ 192.168.80.132:/var/www/***
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica2/imagenes/6.JPG)

Por último, creamos una tarea con cron que se ejecute cada minuto para que se mantenga actualizado el contenido del directorio **/var/www/** entre las máquinas *m1* y *m2*.[Aquí](https://www.techrepublic.com/article/how-to-set-up-auto-rsync-backups-using-ssh/) tenemos un tutorial de como se hace y [aqui](https://www.redeszone.net/2017/01/09/utilizar-cron-crontab-linux-programar-tareas/) otro sobre el uso de crontab.

Editamos el fichero *crontab*, añadiendo una línea con la tarea para que ejecute el comando **ssh 192.168.80.131 rsync -avz -e ssh /var/www/ 192.168.80.132:/var/www/** cada minuto.
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica2/imagenes/7.JPG)

Comprobamos que funciona:
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica2/imagenes/8.JPG)

##Resumen:

Para clonar carpetas entre las dos máquinas hemos seguido estos pasos:
- hemos instalado rsync con el comando **sudo apt-get install rsync**
- hemos generado un par de claves publica y privada para establecer la confianza entre servidores y poder automatizar tareas sin necesidad de introducir contraseñas.
- hemos editado el archivo de configuración de *crontab* añadiendo la siguiente línea **linea en crontab**
	Lo que significa que nuestra máquina sincroniza los archivos de manera automática pasado el tiempo que le indiquemos en el archivo de configuración.

Finalmente ya tenemos replicada la carpeta /var/www/http/ de **m1** en **m2**
