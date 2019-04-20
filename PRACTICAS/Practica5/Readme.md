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
## Replicación mediante configuración maestro-esclavo
## Configuración maestro-maestro

En este [enlace](https://certbot.eff.org/lets-encrypt/ubuntuxenial-nginx) Seleccionando nuestro balanceador y el sistema operativo sobre el que trabajamos, nos facilita una guia de instalación de certbot. Pero no tengo un dominio para poder hacer este ejercicio opcional.

