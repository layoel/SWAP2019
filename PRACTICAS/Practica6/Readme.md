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


Una vez hemos comprobado que funcinona correctamente incluiremos la siguiente al fichero fstab para que se monte la carpeta al inicio cuando reiniciamos la máquina y el usuario no tenga que hacer nada para poder usar los recursos compartidos en esa carpeta.

```bash
elvira@m2~$ sudo nano /etc/fstab

192.168.80.131:/dat/compartida cltem2 nfs auto, noatime, nolock, bg, nfsrvers=3, intr, tcp, actimeo=1800 0 0
```

Podemos obtener información sobre las opciones que podemos añadir al *fstab* haciendo un **man nfs** las que usamos en este caso son:

**actimeo=n** Using actimeo sets all of acregmin, acregmax, acdirmin, and  acdirmax  to  the same value.  If this option is not specified, the NFS client uses the defaults for each of these options listed above.

**bg / fg** Determines how the mount(8) command behaves if an attempt to mount  an  export fails.  The fg option causes mount(8) to exit with an error status if any part of the mount request times out or fails outright.  This  is  called  a  "fore‐ground"  mount,  and  is  the  default behavior if neither the fg nor bg mount option is specified. If the bg option is specified, a timeout or failure causes the  mount(8)  command to fork a child which continues to attempt to mount the export.  The parent immediately returns with a zero exit code. This  is  known  as  a  "back‐ground" mount. If the local mount point directory is missing, the mount(8) command acts as if
the mount request timed out. This permits  nested  NFS  mounts  specified  in /etc/fstab  to proceed in any order during system initialization, even if some NFS servers  are  not  yet  available.   Alternatively  these  issues  can  be
addressed using an automounter (refer to automount(8) for details).

**tcp** The tcp option is an alternative to specifying proto=tcp.  It is included  for
compatibility with other operating systems.

**intr / nointr**  Selects  whether  to  allow signals to interrupt file operations on this mount point. If neither option is specified (or if nointr is specified), signals  do not  interrupt  NFS file operations. If intr is specified, system calls return
EINTR if an in-progress NFS operation is interrupted by a signal. Using the intr option is preferred to using the soft option because it is significantly less likely to result in data corruption. The  intr  /  nointr  mount  option  is  deprecated after kernel 2.6.25.  Only SIGKILL can interrupt a pending NFS operation on these kernels, and if  specified,  this  mount  option  is ignored to provide backwards compatibility with older kernels.

**nfsvers=n** The NFS protocol version number used to contact the server's NFS service.   If the  server  does  not support the requested version, the mount request fails. If this option is not specified, the client negotiates a suitable version with
the server, trying version 4 first, version 3 second, and version 2 last.

**lock / nolock**  Selects whether to use the NLM sideband protocol to lock files on the  server. If  neither option is specified (or if lock is specified), NLM locking is used for this mount point.  When using the nolock  option,  applications  can  lock files,  but  such locks provide exclusion only against other applications running on the same client.  Remote applications are not affected by these locks. NLM locking must be disabled with the nolock option when using  NFS  to  mount /var  because  /var  contains  files  used by the NLM implementation on Linux. Using the nolock option is also required when mounting exports on NFS  servers
that do not support the NLM protocol.
