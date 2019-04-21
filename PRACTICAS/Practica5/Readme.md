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
elvira@m1:~$ mysql -u root -p
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

mysql> 
Database changed
mysql> show tables
    -> ;
Empty set (0,00 sec)

mysql> create table DatosMascotas(IDM int, DNID varchar(10), NombreD varchar(100), NombreM varchar(100), Especie varchar(100), FechaNacimiento varchar(10));
Query OK, 0 rows affected (0,49 sec)
```

Una vez hemos creado nuestra base de datos para la clínica veterinaria y hemos creado la tabla, tenemos que introducir los datos de los animalitos que se tratan en la clínica junto con los datos de sus dueños.

```bash
mysql> insert into DatosMascotas(IDM,DNID,NombreD, NombreM, Especie, FechaNacimiento) values ("1", "12345678A", "Elvira Castillo", "Euler", "Agaporni Personata", "14122018");
Query OK, 1 row affected (0,05 sec)
mysql> insert into DatosMascotas(IDM,DNID,NombreD, NombreM, Especie, FechaNacimiento) values ("2", "12345678A", "Elvira Castillo", "Oli", "Agaporni Fisher", "01022019");
Query OK, 1 row affected (0,02 sec)
mysql> insert into DatosMascotas(IDM,DNID,NombreD, NombreM, Especie, FechaNacimiento) values ("3", "45678954D", "Maria Pereira", "Pluma", "Agaporni Fisher", "15052014");
Query OK, 1 row affected (0,00 sec)
mysql> insert into DatosMascotas(IDM,DNID,NombreD, NombreM, Especie, FechaNacimiento) values ("4", "54785444D", "Jose Lizana", "Peque", "Dogo Aleman", "04082000");
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

Acabamos de realizar la copia de la base de datos de forma manual, vamos a hacerlo de manera automática. Para lo que usaremos el demonio de MySQL, que copia los datos desde un servidor llamado maestro a otro llamado esclavo.

### Empezamos por la configuración del **servidor maestro** que en mi caso será **m1**.
Necesitamos editar el archivo de configuración de MySQL

```BASH
elvira@m1:~$ sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

Tenemos que comentar de ese fichero la linea siguiente para que escuche a un servidor.

```BASH
# bind-address           = 127.0.0.1
```

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/8.JPG)

Y habilitar las lineas siguientes que son las que dicen donde se almacenara el log de errores, el identificador del servidor y donde está el registro binario que tiene toda la información disponible sobre la base de datos.

```BASH
log_error = /var/log/mysql/error.log
server-id               = 1
log_bin                 = /var/log/mysql/ bin.log 
```

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/7.JPG)

Para que los cambios que hemos realizado se apliquen, tenemos que reiniciar el servicio.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/6.JPG)

### Configuración del servidor esclavo  **m2**

Debemos editar el archivo de configuración con los mismos parámetros que para el maestro, con la diferencia del **server-id = 1** que en este caso, para el esclavo debe ser **server-id = 2**

```BASH
elvira@m2:~$ sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
[sudo] password for elvira:
```

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/9.JPG)

Y reiniciamos el servicio.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/10.JPG)

Una vez configurados el maestro y el esclavo, volvemos al servidor maestro para crear un usuario y darle permisos para que haga la replicación.

```BASH
elvira@m1:~$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 3
Server version: 5.7.25-0ubuntu0.16.04.2-log (Ubuntu)

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> create user esclavo identified by 'esclavo';
Query OK, 0 rows affected (0,02 sec)

mysql> grant replication slave on *.* to 'esclavo'@'%' identified by 'esclavo';
Query OK, 0 rows affected, 1 warning (0,01 sec)

mysql> flush privileges;
Query OK, 0 rows affected (0,00 sec)

mysql> flush tables;
Query OK, 0 rows affected (0,00 sec)

mysql> flush tables with read lock;
Query OK, 0 rows affected (0,00 sec)
```

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/11.JPG)

Mostramos los datos del maestro, que los vamos a necesitar en la máquina esclava con la siguiente orden en la consola mysql.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/12.JPG)

La siguiente sentencia la ejecutamos desde el enotorno mysql de la máquina esclava.

```BASH
elvira@m2:~$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 3
Server version: 5.7.25-0ubuntu0.16.04.2-log (Ubuntu)

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> change master to master_host='192.168.80.131', master_user='esclavo', master_password='esclavo', master_log_file='bin.000001', master_log_pos=980, master_port=3306;
Query OK, 0 rows affected, 2 warnings (0,04 sec)

mysql> start slave;
Query OK, 0 rows affected (0,03 sec)

```

Desbloqueamos las tablas de la bd en el maestro:

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/14.JPG)

Probamos que se replica la bd del maestro al esclavo, añadiendo en el maestro (m1) un nuevo dato a la tabla.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/13.JPG)

consultamos el estado del esclavo, con la orden

```BASH
elvira@m2:~$ mysql -u root -p
...
mysql> show slave status\G

*************************** 1. row ***************************
               Slave_IO_State: Waiting for master to send event
                  Master_Host: 192.168.80.131
                  Master_User: esclavo
                  Master_Port: 3306
                Connect_Retry: 60
              Master_Log_File: bin.000001
          Read_Master_Log_Pos: 1314
               Relay_Log_File: m2-relay-bin.000002
                Relay_Log_Pos: 648
        Relay_Master_Log_File: bin.000001
             Slave_IO_Running: Yes
            Slave_SQL_Running: Yes
              Replicate_Do_DB:
          Replicate_Ignore_DB:
           Replicate_Do_Table:
       Replicate_Ignore_Table:
      Replicate_Wild_Do_Table:
  Replicate_Wild_Ignore_Table:
                   Last_Errno: 0
                   Last_Error:
                 Skip_Counter: 0
          Exec_Master_Log_Pos: 1314
              Relay_Log_Space: 852
              Until_Condition: None
               Until_Log_File:
                Until_Log_Pos: 0
           Master_SSL_Allowed: No
           Master_SSL_CA_File:
           Master_SSL_CA_Path:
              Master_SSL_Cert:
            Master_SSL_Cipher:
               Master_SSL_Key:
        Seconds_Behind_Master: 0
Master_SSL_Verify_Server_Cert: No
                Last_IO_Errno: 0
                Last_IO_Error:
               Last_SQL_Errno: 0
               Last_SQL_Error:
  Replicate_Ignore_Server_Ids:
             Master_Server_Id: 1
                  Master_UUID: b0c6959a-41cb-11e9-8ecc-000c297b19c0
             Master_Info_File: /var/lib/mysql/master.info
                    SQL_Delay: 0
          SQL_Remaining_Delay: NULL
      Slave_SQL_Running_State: Slave has read all relay log; waiting for more updates
           Master_Retry_Count: 86400
                  Master_Bind:
      Last_IO_Error_Timestamp:
     Last_SQL_Error_Timestamp:
               Master_SSL_Crl:
           Master_SSL_Crlpath:
           Retrieved_Gtid_Set:
            Executed_Gtid_Set:
                Auto_Position: 0
         Replicate_Rewrite_DB:
                 Channel_Name:
           Master_TLS_Version:
1 row in set (0,00 sec)
```

Realizando esta práctica en la versión inicial me encontré que al llegar aquí, tenía este fallo:

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/15.JPG)

El fallo de la imagen anterior es debido a que cuando cree las máquinas la cloné para seguir con el resto de prácticas y tiene el mismo id en mysql he encontrado [aquí](https://www.beehexa.com/blog/2017/12/17/how-to-fix-master-and-slave-have-equal-mysql-server-uuids-mysql-error/) la solución al problema.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/16.JPG)

Una vez resueltos todos los problemas y habiendo comprobado que funciona la replicación de los datos, ya solo nos queda seguir introduciendo datos en el maestro, y ver que automaticamente se replican en el esclavo.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/17.JPG)

## Configuración maestro-maestro

En este [enlace](https://www.linode.com/docs/databases/mysql/configure-master-master-mysql-database-replication/) tenemos un tutorial para configurar los dos servidores como maestros. [Aquí](https://www.digitalocean.com/community/tutorials/how-to-set-up-mysql-master-master-replication) tenemos otro. Para la configuración he seguido una mezcla de ambos tutoriales.

De nuevo cogeremos las dos máquinas **m1** y **m2** de la práctica1, las he clonado. Esta configuración nos permite que los datos estén replicados entre ambos servidores independientemente de en que servidor sea sobre el que se escriben o modifican los datos. Esto agrega redundancia y aumenta la eficiencia al acceder a los datos.

Comenzaremos con la configuración del servidor **m1** al igual que para el maestro esclavo, tenemos que editar el archivo de configuración de mysql, cambiando las líneas:
- server-id              = 1
- log_bin                = /var/log/mysql/bin.log
- binlog_do_db           = include_database_name
- bind-address           = 127.0.0.1

La primera línea la descomentamos ya que es la que identifica a nuestro servidor con un id único, la segunda línea es el archivo de logs, la tercera línea es la que indica que bases de datos se replicaran entre nuestros servidores y la última línea es la que indica al servidor que acepte conexiones externas a localhost.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/18.JPG)

Reiniciamos el mysql:

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/19.JPG)

Creamos nuestra base de datos, e introducimos algunos datos en la tabla:

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/20.JPG)

Ahora necesitamos crear un usuario que se usará para replicar datos entre m1 y m2.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/21.JPG)

A continuación le damos permisos para que pueda replicar los datos.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/22.JPG)

Consultamos el estado del servidor master en m1.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/23.JPG)

Configuramos mysql en el servidor m2, editamos el archivo de configuración igual que para m1 pero cambiando el id del servidor.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/24.JPG)

Y reiniciamos el servicio para que los cambios se apliquen.

```BASH
elvira@m2:~$ sudo service mysql restart
```

Al igual que en el servidor m1, vamos a crear un  usuario que será el que replique la bd.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/25.JPG)

Y asignamos los permisos para replicar igual que en m1.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/26.JPG)

Ahora usando la informacion de estado del servidor m1, la aplicamos a m2.
```BASH
mysql> change master to master_host='192.168.80.131', master_user='replicator', master_password='password', master_log_file='bin.000001', master_log_pos=2456, master_port=3306;
Query OK, 0 rows affected, 2 warnings (0,29 sec)
```
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/27.JPG)

Si nos fijamos, hasta aqui, todo es igual que cuando instalamos el servidor maestro esclavo. A continuación tomaremos nota de los valores de MASTER LOG FILE y MASTER LOG POS del servidor m2 para añadirlos al servidor m1 como si ahora m1 fuera el esclavo.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/28.JPG)


insert into DatosMascotas(IDM,DNID,NombreD, NombreM, Especie, FechaNacimiento) values ("6", "12352145W", "Alejandro Jeronimo", "Pichi", "Pollito", "13012016");