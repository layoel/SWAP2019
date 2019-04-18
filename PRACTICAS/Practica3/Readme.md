# Práctica 3: Balanceo de carga

## NGINX Balanceo por turnos
Inicialmente tenemos que crear una nueva maquina virtual con ubuntu server que hará las funciones de balanceador, este equipo se llama LB la  IP de mi balanceador es 192.168.80.133 está en red con las maquinas m1 y m2

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/1.JPG)

En esta máquina no hemos hecho como en las anteriores en la instalación unicamente hemos marcado el servicio ssh y no hemos instalado LAMP para poder tener libre el puerto 80 que es el que se usará para el balanceo de carga.

Vamos a instalar *nginx* escribiendo en consola:
*elvira@LB:~$ **sudo apt-get install nginx***
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/2.JPG)
Una vez instalado el servicio, lo iniciamos:
*elvira@LB:~$ **sudo systemctl start nginx***
En el navegador podemos ver que el nginx está funcionando.
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/4.JPG)

A continuación, configuraremos nginx para ello modificamos el fichero de configuración que está en */etc/nginx/conf.d/default.conf*
*elvira@LB:~$ **sudo nano /etc/nginx/conf.d/default.conf***
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/3.JPG)

Al editar este fichero, hemos configurado nuestro balanceador de carga con el algoritmo por turnos *round-robin* para que los cambios se apliquen, reiniciamos el servicio con:
*elvira@LB:~$ **sudo service nginx restart***
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/5.JPG)

Si al hacer el curl desde otra máquina (dentro de la misma red) nos aparece la web principal de nginx en lugar de las webs de los servidores m1 y m2, tendremos que modificar el fichero *nginx.conf* comentando la línea donde dice **include /etc/nginx/sites-enabled**. La ruta del fichero es */etc/nginx/nginx.conf*
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/6.JPG)

Una vez realizada la modificación anterior volveremos a reiniciar el servicio.

Podemos comprobar con *curl 192.168.80.133* o bien escribiendo la ip del balanceador en nuestro navegador. Veremos que por turnos responde uno u otro servidor web. He desactivado la copia de la carpeta /var/www/http y editado el fichero index en ambos servidores para ver que servidor responde a la petición.
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/7.JPG)
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/8.JPG)

## NGINX Balanceo por ponderación
Éste algoritmo lo usaremos cuando una de las máquinas sea más potente que la otra. Para ello en el archivo de configuración en la parte del upstream añadiremos el modificador **weight** con un número que será el que indicará la carga que asignamos a ese servidor web.
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/9.JPG)
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/10.JPG)
Con esta modificación cargamos más un servidor que otro de peticiones pero nos interesa que las peticiones que vengan de la misma ip lleguen a la misma maquina servidora final. Para conseguir eso tenemos que balancear por IP y eso se hace modificando el archivo de configuración añadiendo la directiva **ip_hash**
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/11.JPG)
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/12.JPG)

Podemos usar la directiva *keepalive* para que el tiempo de mantenimiento de la conexión sea el fijado por nosotros en el fichero de configuración, así evitaremos el problema que surge a los usuarios que están tras un proxy o un nat, para que no sean dirigidos siempre al mismo backend y se equilibre el balanceo.
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/13.JPG)
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/14.JPG)

Con **ip_hash** podemos añadir junto al servidor la directiva *down* que lo pone como desconectado.
Tambien la directiva *backup* pero sin **ip_hash** que hace que el servidor aparezca como respaldo y solo sirva peticiones en caso de que el resto de servidores estén caidos y ocupados.
Podemos añadir el número máximo de fallos *max_fails* y el tiempo en el que se considera un servidor que no responde con *fail_timeout =tiempo*

## HAPROXY Balanceo por turnos
En lugar de como dice el guión, parar el servicio de nginx e instalar haproxy, he decidido crear otra maquina virtual con el servicio, cuya direccion IP es **192.168.80.135**.
En este [enlace](http://www.maestrosdelweb.com/balance-de-carga-haproxy/) escrito en español, tenemos una guia de instalación, configuración y prueba de instalación y conclusiones.Al igual que en la web oficial de [haproxy](http://www.haproxy.org/) en inglés.

Lo primero que hay que hacer es instalar el servicio. Para ello ejecutamos el comando:
*elvira@LB2:~$ **sudo apt-get install haproxy***

Una vez instalado, tenemos que modificar el archivo de instalación para que el balanceador acepte conexiones entrantes por el puerto 80 y las reenvie a los dos servidores web **m1** y **m2** 
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/15.JPG)

Ahora iniciamos el servicio haproxi con el comando.
*elvira@LB2:~$ **sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg***

A continuación si no nos ha dado ningún fallo el iniciar el servicio ya podemos ejecutar el curl y veremos que haproxy está haciendo de balanceador entre m1 y m2 usa el balanceo por turnos.
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/16.JPG)
## HAPROXY Balanceo por ponderación
Si queremos usar un algoritmo basado en ponderación debemos añadir en el fichero de configuración haproxy.cfg los pesos de las conexiones que va a soportar cada servidor.
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/17.JPG)
Para que los cambios se apliquen debemos reiniciar el servicio de nuevo. Y comprobamos desde otra máquina como funciona este algoritmo de balanceo aplicado con haproxy.
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/18.JPG)

## POUND Balanceo por turnos

La máquina creada como balanceador con Pound tiene la ip **192.168.80.136**
Hay diversos tutoriales como [este](https://linuxtechlab.com/load-balancing-web-servers-using-pound-load-balancer/) que indican como instalar y configurar pound en servidores centos, pero dado que mi servidor es un ubuntu server, usaremos este [enlace](https://help.ubuntu.com/community/Pound) de la ayuda de ubuntu donde explican como configurarlo e instalarlo. También podemos ver todas las opciones que tiene para configurar pound en el **man page pound(8)** donde además tenemos ejemplos del archivo de configuración.

Primero instalamos el servicio con:
*elvira@LB-POUND:~$**sudo apt-get install pound***
Una vez instalado, al igual que en los casos anteriores, tenemos que editar el fichero de configuración del servicio *pound.cfg* situado en:

*elvira@LB-POUND:~$**sudo nano /etc/pound/pound.cfg***
el archivo de configuración original lo he copiado para no perderlo
*elvira@LB-POUND:~$**sudo cp /etc/pound/pound.cfg /etc/pound/pound-copy.cfg***
y a continuación he editado el fichero añadiendo las ip de los dos servidores web y la ip del balanceador y el puerto 80 que es donde escuchan peticiones.
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/19.JPG)

Como siempre, una vez editado el fichero de configuración reiniciaremos el servicio para que los cambios tengan efecto. Pero antes hay que tener en cuenta que hay que cambiar en **/etc/default/pound** la variable startup a 1
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/20.JPG)
ahora si, reiniciamos el servicio.
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/21.JPG)

Por último solo nos queda comprobar el balanceo por turnos con pound, podemos hacerlo como en los anteriores con curl.
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/22.JPG)

## Someter a una alta carga el servidor balanceado

Para poder lleva a cabo esta tarea, vamos a usar la herramienta *Apache Benchmark* que nos dará los resultados de rendimiento de nuestra granja web.

Para empezar, como dispongo de 3 maquinas con cada uno de los balanceadores, tengo que instalar la utilidad de apache benchmark en dos de ellos para probarla despues de para el servicio de balanceador en la maquina donde este ejecutando la herramienta de benchmark.

*elvira@LB:~$**sudo apt-get install apache2-utils***
*elvira@LB-POUND:~$**sudo apt-get install apache2-utils***

Una vez instalado en uno de las maquinas por ejemplo en la que tengo instalado Pound, paro el servicio como vimos en el apartado anterior. Y ejecutamos el benchmark para nginx con la siguiente orden:

*elvira@LB-POUND:~$**sudo apt-get install apache2-utils***
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/23.JPG)
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica3/imagenes/24.JPG)

// salida haproxy
~~
This is ApacheBench, Version 2.3 <$Revision: 1706008 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking 192.168.80.135 (be patient)


Server Software:        Apache/2.4.18
Server Hostname:        192.168.80.135
Server Port:            80

Document Path:          /index.html
Document Length:        78 bytes

Concurrency Level:      100
Time taken for tests:   62.788 seconds
Complete requests:      100000
Failed requests:        0
Total transferred:      34700000 bytes
HTML transferred:       7800000 bytes
Requests per second:    1592.66 [#/sec] (mean)
Time per request:       62.788 [ms] (mean)
Time per request:       0.628 [ms] (mean, across all concurrent requests)
Transfer rate:          539.70 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0   19  16.2     20    1025
Processing:     2   44  86.1     36    3054
Waiting:        1   36  86.1     28    3038
Total:          2   63  87.1     58    3057

Percentage of the requests served within a certain time (ms)
  50%     58
  66%     60
  75%     62
  80%     63
  90%     67
  95%     78
  98%    130
  99%    275
 100%   3057 (longest request)
~~

-------------------------------------------------------------------

// salida nginx
~~

This is ApacheBench, Version 2.3 <$Revision: 1706008 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking 192.168.80.133 (be patient)


Server Software:        nginx/1.10.3
Server Hostname:        192.168.80.133
Server Port:            80

Document Path:          /index.html
Document Length:        78 bytes

Concurrency Level:      100
Time taken for tests:   98.521 seconds
Complete requests:      100000
Failed requests:        0
Total transferred:      34600000 bytes
HTML transferred:       7800000 bytes
Requests per second:    1015.01 [#/sec] (mean)
Time per request:       98.521 [ms] (mean)
Time per request:       0.985 [ms] (mean, across all concurrent requests)
Transfer rate:          342.96 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    1   1.3      1     209
Processing:     1   98  48.6     89    1094
Waiting:        1   97  48.6     88    1093
Total:          2   98  48.6     89    1095

Percentage of the requests served within a certain time (ms)
  50%     89
  66%     92
  75%    108
  80%    111
  90%    115
  95%    120
  98%    153
  99%    247
 100%   1095 (longest request)
~~
 -----------------------------------------------------------------------------
// pound benchmark
~~
This is ApacheBench, Version 2.3 <$Revision: 1706008 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking 192.168.80.136 (be patient)


Server Software:        Apache/2.4.18
Server Hostname:        192.168.80.136
Server Port:            80

Document Path:          /index.html
Document Length:        78 bytes

Concurrency Level:      100
Time taken for tests:   98.348 seconds
Complete requests:      100000
Failed requests:        0
Total transferred:      34700000 bytes
HTML transferred:       7800000 bytes
Requests per second:    1016.79 [#/sec] (mean)
Time per request:       98.348 [ms] (mean)
Time per request:       0.983 [ms] (mean, across all concurrent requests)
Transfer rate:          344.56 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0   38  12.5     37    1041
Processing:     3   60  29.6     57    1101
Waiting:        2   44  28.6     43    1085
Total:          4   98  32.2     93    1143

Percentage of the requests served within a certain time (ms)
  50%     93
  66%    100
  75%    105
  80%    110
  90%    120
  95%    130
  98%    143
  99%    151
 100%   1143 (longest request)
~~
A modo de resumen veamos una tabla comparativa de la ejecución del benchmark en los 3 balanceadores:
|---------------|:-----------------------------------------------------------:|------------------|--------------------|
|               | **Time**                                                    |                  |                    |
|**Balanceador**|:-------------------------------------------------------------:|**Failed Request**|**Request per sec.**|
|               |*Time taken for test*|*time per req. min.*|*time per req.max.*|                  |                    |
|:-------------:|:-------------------:|:------------------:|:-----------------:|:----------------:|:------------------:|
|**NGINX**|98.521|0.985|98.521|0|1015.01|
|**HAPROXY**|62.788|0.628|62.788|0|1592.66|
|**POUND**|98.348|0.983|98.348|0|1016.79|
|----------|----------|----------|----------|

Como podemos deducir de la tabla comparativa de los tres Balanceadores, si tuviera que implementarlo para una empresa que se dedique a servir páginas web yo elegiría Haproxy porque los resultados en tiempos/numero de peticiones son mucho mejores. Podemos ver que Nginx y Pound están muy igualados en tiempos de respuesta y numero de peticiones. Dado que la web que hemos servido es muy simple probablemente por eso el numero de fallos para los tres balanceadores es 0.

##Resumen:

-