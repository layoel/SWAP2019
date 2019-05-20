# Práctica 6: Servidor de disco NFS

Los objetivos que se quieren conseguir con esta práctica son:
- Configurar una máquina como servidor de disco NFS y exportar una carpeta a los clientes.
- Montar en las máquinas cliente la carpeta exportada por el servidor.
- Comprobar que la información que se escribe en una máquina en dicha carpeta se ve actualizada en el resto de máquinas que comparten ese espacio.

## Configurar el servidor NFS
Para esta práctica voy a usar dos máquinas, una será m1 con la ip 192.168.80.131 y la otra será m2 con la ip 192.168.80.132

Para empezar en m1 que será la máquina principal donde configuraremos el sistema de archivos, instalaremos las herramientas que necesitamos:

```bash
elvira@m1:~$ sudo apt-get install nfs-kernel-server nfs-common rpcbind
```

Una vez instalado crearemos la carpeta que contendrá los archivos compartidos.

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica6/imagenes/1.JPG)

Para que pueda acceder a la carpeta compartida cualquier usuario tenemos que editar el dueño y los permisos de esa carpeta:

![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica6/imagenes/2.JPG)




## Configurar los clientes

```bash

```




## Replicar una BD MySQL con mysqldump





![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/2.JPG)



## Replicación mediante configuración maestro-esclavo


```BASH

```


![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica5/imagenes/8.JPG)

