# Práctica 5: Replicación de bases de datos MySQL

Los objetivos que se quieren conseguir con esta práctica son:
- Copiar archivos de copia de seguridad mediante ssh.
- Clonar manualmente BD entre máquinas.
- Configurar la estructura maestro-esclavo entre dos máquinas para realizar el clonado automático de la información.

## Crear tar y copiarlos en remoto

Para esta práctica usaré de nuevo los servidores web **m1** (192.168.80.131), **m2** (192.168.80.132) de la práctica1.

Como vimos en la práctica 1 podemos copiar archivos entre servidores con **tar** o bien con **scp**
```bash
elvira@m1:~$ tar czf - ./tar.tgz | ssh 192.168.80.132 'cat > ~/tar.tgz'
```
Pero para copiar bases de datos hay otras formas de hacerlo, lo veremos a continuación.


## Crear BD e insertar datos

Vamos a crear una base de datos imaginando que se trata de un veterinario, por lo que necesitamos una tabla llamada DatosMascotas con las columnas IDM, DNID, NombreD, NombreM, Especie y FechaNacimiento.

```bash
elvira@m1:~$ mysql -uroot -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 3
Server version: 5.7.25-0ubuntu0.16.04.2 (Ubuntu)

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> create database mascotas;
Query OK, 1 row affected (0,05 sec)

mysql> use mascotas
Database changed
mysql> show tables
    -> ;
Empty set (0,00 sec)

mysql> create table DatosMascotas(IDM int, DNID varchar(9), NombreD varchar(100), NombreM varchar(100), Especie varchar(100), FechaNacimiento varchar(10));
Query OK, 0 rows affected (0,49 sec)
```
Una vez hemos creado nuestra base de datos para la clínica veterinaria y hemos creado la tabla, tenemos que introducir los datos de los animalitos que se tratan en la clínica junto con los datos de sus dueños.

```bash
mysql> insert into DatosMascotas(IDM,DNID,NombreD, NombreM, Especie, FechaNacimiento) values ("1", "123456789A", "Elvira Castillo", "Euler", "Agaporni Personata", "14122018");
Query OK, 1 row affected (0,05 sec)
mysql> insert into DatosMascotas(IDM,DNID,NombreD, NombreM, Especie, FechaNacimiento) values ("2", "123456789A", "Elvira Castillo", "Oli", "Agaporni Fisher", "01022019");
Query OK, 1 row affected (0,02 sec)
mysql> insert into DatosMascotas(IDM,DNID,NombreD, NombreM, Especie, FechaNacimiento) values ("3", "456789554D", "Maria Pereira", "Pluma", "Agaporni Fisher", "15052014");
Query OK, 1 row affected (0,00 sec)
mysql> insert into DatosMascotas(IDM,DNID,NombreD, NombreM, Especie, FechaNacimiento) values ("4", "547885444D", "Jose Lizana", "Peque", "Dogo Aleman", "04082000");
Query OK, 1 row affected (0,00 sec)

```

Podemos ver las tablas que pertenecen a la base de datos mascotas y ver el contenido de la tabla que queramos.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/1.JPG)


## Replicar una BD MySQL con mysqldump

Para esta parte de la práctica vamos a usar la herramienta **mysqldump** con la que vamos a realizar un volcado de la base de datos "mascotas" creada con anterioridad. Vamos a ver que opciones tiene la herramienta, para ello ejecutamos el comando:

```bash
elvira@m1:~$ mysqldump --help
```
Para poder hacer la copia de seguridad, primero tenemos que evitar que se acceda a la Base de datos para cambiar nada, para que los datos sean correctos a la hora de hacer la copia y no pueda haber problemas de inconsistencia de datos. Para eso ejecutaremos lo siguente:

```bash
elvira@m1:~$ mysql -u root -p
mysql> flush tables with read lock;
Query OK, 0 rows affected (0,06 sec)

mysql> quit
```

Ahora usaremos **mysqldump** para hacer copia de los datos.
```bash
elvira@m1:~$ sudo mysqldump mascotas -u root -p > /tmp/copymascotas.sql
```
Nos pide la contraseña del usuario y de root, pero finalmente hace una copia en la carpeta que hemos indicado.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/2.JPG)

Una vez realizada la copia, tenemos que desbloquear las tablas de la base de datos para que puedan seguir modificandose o insertandose datos en la BD.

```bash
elvira@m1:~$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 9
Server version: 5.7.25-0ubuntu0.16.04.2 (Ubuntu)

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> unlock tables;
Query OK, 0 rows affected (0,00 sec)

mysql> quit
Bye
```
Como ya tenemos la copia ahora hay que pasarla al servidor **m2**, la copiaremos como ya sabemos o bien con rsync o con scp.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/4.JPG)

Si nos fijamos el archivo que se ha copiado incluye las sentencias sql de creación de la tabla y de introducción de los datos, pero no aparece la creación de la base de datos mascotas.

```BASH
elvira@m2:~$ cat ./copymascotas.sql
-- MySQL dump 10.13  Distrib 5.7.25, for Linux (x86_64)
--
-- Host: localhost    Database: mascotas
-- ------------------------------------------------------
-- Server version       5.7.25-0ubuntu0.16.04.2

/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8 */;
/*!40103 SET @OLD_TIME_ZONE=@@TIME_ZONE */;
/*!40103 SET TIME_ZONE='+00:00' */;
/*!40014 SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 */;
/*!40014 SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 */;
/*!40101 SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' */;
/*!40111 SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0 */;

--
-- Table structure for table `DatosMascotas`
--

DROP TABLE IF EXISTS `DatosMascotas`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `DatosMascotas` (
  `IDM` varchar(100) DEFAULT NULL,
  `DNID` varchar(10) DEFAULT NULL,
  `NombreD` varchar(100) DEFAULT NULL,
  `NombreM` varchar(100) DEFAULT NULL,
  `Especie` varchar(100) DEFAULT NULL,
  `FechaNacimiento` varchar(100) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `DatosMascotas`
--

LOCK TABLES `DatosMascotas` WRITE;
/*!40000 ALTER TABLE `DatosMascotas` DISABLE KEYS */;
INSERT INTO `DatosMascotas` VALUES ('1','123456789A','Elvira Castillo','Euler','Agaporni Personata','14122018'),('2','123456789A','Elvira Castillo','Oli','Agaporni Fisher','01022019'),('3','456789554D','Maria Pereira','Pluma','Agaporni Fisher','15052014'),('4','547885444D','Jose Lizana','Peque','Dogo Aleman','04082000');
/*!40000 ALTER TABLE `DatosMascotas` ENABLE KEYS */;
UNLOCK TABLES;
/*!40103 SET TIME_ZONE=@OLD_TIME_ZONE */;

/*!40101 SET SQL_MODE=@OLD_SQL_MODE */;
/*!40014 SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS */;
/*!40014 SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS */;
/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
/*!40111 SET SQL_NOTES=@OLD_SQL_NOTES */;

-- Dump completed on 2019-04-20 23:44:03
elvira@m2:~$
```

Para poder restaurar la BD en **m2** tendremos que crear primero la base de datos:

```BASH
elvira@m2:~$ mysql -u root -p
.......
mysql> create database `mascotas`;
Query OK, 1 row affected (0,08 sec)
mysql> quit
Bye
```

A continuación, restauramos los datos de la BD que están en el script sql que copiamos de m1 a m2. Y comprobamos que está correcta.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/5.JPG)

## Replicación mediante configuración maestro-esclavo

Para realizar la copia de manera automática, usaremos el demonio de MySQL, que copia los datos desde un servidor llamado maestro a otro llamado esclavo.

### Empezamos por la configuración del **servidor maestro** que en mi caso será **m1**.
Necesitamos editar el archivo de configuración de MySQL

```BASH
elvira@m1:~$ sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

Tenemos que comentar de ese fichero la linea siguiente para que escuche a un servidor.

```BASH
# bind-address           = 127.0.0.1
```

Y habilitar las lineas siguientes que son las que dicen donde se almacenara el log de errores, el identificador del servidor y donde está el registro binario que tiene toda la información disponible sobre la base de datos.

```BASH
log_error = /var/log/mysql/error.log
server-id               = 1
log_bin                 = /var/log/mysql/mysql-bin.log
```
Para que los cambios que hemos realizado se apliquen, tenemos que reiniciar el servicio.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/6.JPG)

### Configuración del esclavo 



## Configuración maestro-maestro




En este [enlace](https://certbot.eff.org/lets-encrypt/ubuntuxenial-nginx) Seleccionando nuestro balanceador y el sistema operativo sobre el que trabajamos, nos facilita una guia de instalación de certbot. Pero no tengo un dominio para poder hacer este ejercicio opcional.

