# Práctica 6: Servidor de disco NFS

Los objetivos que se quieren conseguir con esta práctica son:
- Configurar una máquina como servidor de disco NFS y exportar una carpeta a los clientes.
- Montar en las máquinas cliente la carpeta exportada por el servidor.
- Comprobar que la información que se escribe en una máquina en dicha carpeta se ve actualizada en el resto de máquinas que comparten ese espacio.

## Configurar el servidor NFS
Para esta práctica voy a usar dos máquinas, una será m1 con la ip 192.168.80.131. Uno de los clientes m2 con la ip 192.168.80.132 y m3 será otro de los clientes con la ip 192.168.80.144

Para empezar en m1 que será la máquina principal donde configuraremos el sistema de archivos, instalaremos las herramientas que necesitamos:

```bash
elvira@m1:~$ sudo apt-get install nfs-kernel-server nfs-common rpcbind
```

Una vez instalado crearemos la carpeta que contendrá los archivos compartidos.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica6/imagenes/1.JPG)

Para que pueda acceder a la carpeta compartida cualquier usuario tenemos que editar el dueño y los permisos de esa carpeta:

```bash
elvira@m1:~$ sudo chown nobody:nogroup /dat/compartida/
elvira@m1:~$ sudo chmod -R 777 /dat/compartida/
```
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica6/imagenes/2.JPG)

Debemos editar el archivo de configuración y añadir las ip de las máquinas que tendrán acceso al sistema de archivos compartido y pondremos que pueden hacer en ese sistema, es decir si tienen permiso de lectura o de lectura y escritura...

```bash
elvira@m1:~$ nano /etc/export
```
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica6/imagenes/3.JPG)

Para que los cambios se apliquen tenemos que reiniciar el servicio.

```bash
elvira@m1:~$ sudo service nfs-kernel-server restart
```

## Configurar los clientes

Mis clientes serán m2 y m3. Tenemos que actualizar e instalar en cada una de las máquinas los siguientes paquetes:

```bash
sudo apt update
sudo apt-get install nfs-common rpcbind
```

Creamos la carpeta donde vamos a montar el sistema de archivos.

```bash
elvira@m2:~$ mkdir cltem2

elvira@m3~$ mkdir cltem3
```
En m3 creo la carpeta y cambio los permisos

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica6/imagenes/4.JPG)

En m2 hago lo mismo

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica6/imagenes/6.JPG)


Monto los archivos compartidos en la carpeta que acabo de crear.

En m3:
```bash
elvira@m3~$ sudo mount 192.168.80.131:/dat/compartida cltem3
```
creamos un fichero de prueba en esa carpeta y comprobamos si está en la carpeta compartida de m1

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica6/imagenes/5.JPG)

En m2:
```bash
elvira@m2~$ sudo mount 192.168.80.131:/dat/compartida cltem2
```
Para comprobar que funciona la carpeta compartida entre los 3 servidores, en m2 he creado un nuevo directorio dentro de la carpeta compartida y un nuevo fichero de texto y vemos que en m3 aparece replicado

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica6/imagenes/8.JPG)
