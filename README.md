# EJERCICIOS DE SWAP 2019

# Tema1

## Ejercicio 1.1 
### Buscar información sobre las tareas o servicios web para los que se usan más los programas:

- **Apache**: La wikipedia define " Apache es un servidor web HTTP de código abierto, para plataformas Unix (BSD, GNU/Linux, etc.)" La web oficial de [Apache](https://httpd.apache.org/) podemos encontrar  toda la documentación necesaria para instalar y configurar un servidor con Apache. Si indagamos un poco por la red podemos ver que algunas empresas importantes que usan apache incluyen a Cisco, IBM, Salesforce, General Elecctric Adobe, VMWare, Xerox, Linkedln, Facebook, Hewlett-Packard, At & T, Siemens, Ebay y más.[fuente](https://kinsta.com/es/base-de-conocimiento/que-es-apache/). 

- **Nginx**: También es un servidor web de código abierto, ahora también es usado como proxy inverso, caché de HTTP y balanceador de carga. La versión mas actual de Nginx es la 3.1 Mejora las funcionalidades de apache por ejemplo para sitios web estáticos o sitios web con alto tráfico. La web oficial de [nginx](https://www.nginx.com/). Originalmente fue creado por Igor Sysoev y apareció en público en octubre de 2004. Es una opción Opensource de alto rendimiento, muy ligera y flexible. Su característica principal es la asincronía. Nginx mejora el rendimiento de webs con respecto a Apache en cuanto a concurrencia, dado que es capaz de administrar más accesos concurentes de lo que lo podría hacer Apache y empleando menores requisitos de memoria.

- **thttpd**: Su [web oficial](http://acme.com/) nos dice que es un servidor web de código libre disponible para la mayoría de versiones unix. Sus características principales son que es simple, pequeño, portatil, rápido y seguro ya que utiliza los requerimientos mínimos de un servidor HTTP. Por ese motivo es ideal para servir grandes volúmenes de datos de información estática.[fuente](https://es.wikipedia.org/wiki/Thttpd) Podemos acceder a todas las opciones de configuración en el manual de linux [*man page thttpd(8)*](https://linux.die.net/man/8/thttpd) Los desarrolladores de este servidor son ACME Laboratories.

- **Cherokee**: En la [web oficial](http://cherokee-project.com/) nos definen cherokee como un servidor web de código abierto, innovador, rico en funciones, increiblemente rápido y fácil de configurar, diseñado para aplicaciones web seguras altamente concurrentes. Su configuración se hace a través de una interfaz web y nos dicen que es compatible con tecnologías como FastCGI,SCGI, PHP, uWSGI, SSI, CGI, LDAP, TLS/SSL, proxy HTTP, transmisión de vídeo, almacenamiento en caché de contenidos, configuración de tráfico... etc. Se puede ejecutar en Linux, MAC OS X, Solaris y BSD.

- **node.js**:La [web oficial de nodejs](https://nodejs.org/en/docs/guides/getting-started-guide/) nos dice que Node está diseñado para crear aplicaciones de red escalables. Nos permite manejar muchas conexiones al mismo tiempo. Una característica importante de Node es que no existen bloqueos porque casi ninguna funcion en Node se realiza sobre entrada/salida. Esto hace que sea el servidor web ideal cuando necesitamos escalabilidad. Node.js funciona en javascript, por lo que podemos usar este mismo lenguaje en el frontend y en el backend.

--------------------------------------------------------

# Tema2

## Ejercicio 2.1 
### Calcular la disponibilidad del sistema si tenemos dos réplicas de cada elemento (en total 3 elementos en cada subsistema).

Para calcular la disponibilidad con 1 replica usamos la formula *As = Acn-1 + ( (1 – Acn-1) * Acn )*

Donde: 
- **As** es la disponibilidad final.
- **Ac_n-1** es la disponibilidad antes de añadir la siguiente réplica.
- **Ac_n** es la disponibilidad del servidor que vamos a añadir.

| **Component**   |   **Disponibilidad incial** |   **disponibilidad 1 replica** |   **disponibilidad 2 replicas** |
|:------------:|:---------------:|:----------------:|:----------------:|
| **Web**         |   **0.850000000** |     *0.977500000* |     *0.996625000* |
| **Application** |   **0.900000000** |     *0.990000000* |     *0.999000000* |
| **Database**    |    **0.999000000** |     *0.999999000* |     *0.999999999* |
| **DNS**         |    **0.980000000** |     *0.999600000* |     *0.999992000* |
| **Firewall**    |    **0.850000000** |     *0.977500000* |     *0.996625000* |
| **Switch**      |    **0.990000000** |     *0.999900000* |     *0.999999000* |
| **Datacenter**  |    **0.999900000** |     *0.999900000* |     *0.999900000* |
| **ISP**         |    **0.950000000** |     *0.997500000* |     *0.999875000* |

## Ejercicio 2.2 
### Buscar frameworks y librerías para diferentes lenguajes que permitan hacer aplicaciones altamente disponibles con relativa facilidad. Como ejemplo, examina PM2 [*https://github.com/Unitech/pm2* ](https://github.com/Unitech/pm2) que sirve para administrar clústeres de NodeJS.

- [Frameworks para desarrollo web con PHP](https://www.wearemarketing.com/es/blog/frameworks-en-el-desarrollo-web-las-mejores-practicas-para-tu-negocio-online.html#):

	- [*Symfony 4*](https://www.hostinger.es/tutoriales/mejores-frameworks-php/): Es el preferido por muchos desarrolladores web. Está compuesto por componentes que se pueden reutilizar y tiene una comunidad activa que expone nuevos códigos para el desarrollo de mejoras en actualizaciones. Tiene licencia libre, te da la capacidad de controlar accesos a la informacion, permite la creación de app en distintos idiomas, la facilidad de uso de su arquitectura y los diseños comprensibles y fáciles de usar para los desarrolladores web hacen que el código de este framework sea de calidad.
	- [*Laravel*](https://www.hostinger.es/tutoriales/mejores-frameworks-php/): Este framework es conocido por su sintaxis que es fácil de entender y fácil para trabajar con ella. El núcleo de Laravel es sólido desde el punto de vista del rendimiento y se puede ampliar usando muchas extensiones. Se integra con otras bibliotecas y plataformas como AWS para crear aplicaciones altamente escalables. Se puede ejecutar de forma asincrona y eso hace que aumente el rendimiento. Además tiene integradas funciones para manejar el enrutamiento, la administración de usuarios y el almacenamiento caché.
	- [*CakePHP*](https://www.hostinger.es/tutoriales/mejores-frameworks-php/): fue el primer framework en salir al mercado con el tipo de arqiutectura de modelo vista controlador. Tiene bibliotecas que incluyen cantidad de componentes útiles, esto hace que puedas programar proyectos más rápidamente.
	- [*CodeIgniter*](https://www.hostinger.es/tutoriales/mejores-frameworks-php/): Es un framework PHP que usa una arquitectura de modelo vista controlador. Usa diferentes componentes para manejar tareas de desarrollo específicas. Usa un framework ligero pensado para mejorar el rendimiento, tiene una documentación que hace fácil su uso.
	- [*Yii*](https://www.hostinger.es/tutoriales/mejores-frameworks-php/): yes it is!, sobresale en comparación con otros porque es muy fácil instalarlo. Ayuda con sus componentes adicionales a acelerar el desarrollo de aplicaciones web. Tiene un conjunto de caracteristicas de seguridad que hace que tus aplicaciones y tus proyectos sean altamente seguros.
	- [*FuelPHP*](https://www.hostinger.es/tutoriales/mejores-frameworks-php/): tiene soporte completo para HMVC. De forma predeterminada la seguridad que implementa a tus aplicaciones es fuerte. Una carácteristica que lo diferencia de los demás es que tiene una función de línea de comandos única. Soporta versiones superiores a PHP 5.4 y tiene documentación detalada que ayuda a agilizar el desarrollo.
- Frameworks para web con Python:
	- [*Django*](https://hackernoon.com/top-10-python-web-frameworks-to-learn-in-2018-b2ebab969d1a)
	- [*Pyramid*](https://hackernoon.com/top-10-python-web-frameworks-to-learn-in-2018-b2ebab969d1a)
	- [*web2py*](https://hackernoon.com/top-10-python-web-frameworks-to-learn-in-2018-b2ebab969d1a)
	- [*Flask*](https://hackernoon.com/top-10-python-web-frameworks-to-learn-in-2018-b2ebab969d1a)
	- [*Bottle*](https://hackernoon.com/top-10-python-web-frameworks-to-learn-in-2018-b2ebab969d1a)
	- [*Tornado*](https://hackernoon.com/top-10-python-web-frameworks-to-learn-in-2018-b2ebab969d1a)
- [Frameworks para web con java](https://openwebinars.net/blog/los-7-mejores-frameworks-de-java/):
	- [*Spring MVC*](https://openwebinars.net/blog/los-7-mejores-frameworks-de-java/):
	- [*Struts 2*](https://openwebinars.net/blog/los-7-mejores-frameworks-de-java/):
	- [*Hibernate*](https://openwebinars.net/blog/los-7-mejores-frameworks-de-java/):
	- [*Vaadin*](https://openwebinars.net/blog/los-7-mejores-frameworks-de-java/)
	- [*Goggle Web Toolkit*](https://openwebinars.net/blog/los-7-mejores-frameworks-de-java/)
	- [*Grails*](https://openwebinars.net/blog/los-7-mejores-frameworks-de-java/)

## Ejercicio 2.3
### ¿Cómo analizar el nivel de carga de cada uno de los subsistemas en el servidor? Buscar herramientas y aprender a usarlas. ...¡o recordar cómo usarlas!

- [Monitorización de servidor linux por consola](https://openwebinars.net/blog/3-formas-de-monitorizar-servidores-linux/)
	- top
	- htop
	- dstat
	- ps
	- lsof
	- netsat
	- route
	- iptraf
	- iftop
	- df
	- iotop

- [Monitorización de un servidor Linux: Aplicaciones de interfaz web](https://openwebinars.net/blog/3-formas-de-monitorizar-servidores-linux/)
	- cacti
	- munin
	- collectd
- [Monitorización de infraestructuras](https://openwebinars.net/blog/3-formas-de-monitorizar-servidores-linux/)
	- Nagios
	- Zabix

## Ejercicio 2.4
### Buscar ejemplos de balanceadores software y hardware (productos comerciales).
### Buscar productos comerciales para servidores de aplicaciones.
### Buscar productos comerciales para servidores de almacenamiento.

--------------------------------------------------------

# Tema3

## Ejercicio 3.1 
### Buscar con qué órdenes de terminal o herramientas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.

## Ejercicio 3.2 
### Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.

----------------------------------------------------------------------
# Tema4

## Ejercicio 4.1
###Buscar información sobre cuánto costaría en la actualidad un mainframe que tuviera las mismas prestaciones que una granja web con balanceo de carga y 10 servidores finales (p.ej).

## Ejercicio 4.2
### Buscar información sobre precio y características de balanceadores comerciales (hardware) específicos. Compara las prestaciones que ofrecen unos y otros.

## Ejercicio 4.3
### Instala y configura en una máquina virtual el balanceador ZenLoadBalancer. Compara con la dificultad de la instalación y configuración usando nginx o haproxy (práctica 3).

## Ejercicio 4.4 
### Implementar un pequeño servicio web en los servidores finales que devuelva el % CPU y % RAM que en un instante tiene en uso dicho servidor. Lo debe devolver como una cadena de texto plano que representa ambos porcentajes, p.ej: “CPU 45% RAM 76%”

## Ejercicio 4.5
### Buscar información sobre los métodos de balanceo que implementan los dispositivos recogidos en el ejercicio 4.2 (o el software que hemos propuesto para la práctica 3).

## Ejercicio 4.6 
### Probar las diferentes maneras de redirección HTTP. ¿Cuál es adecuada y cuál no lo es para hacer balanceo de carga global? ¿Por qué?

## Ejercicio 4.7 
### Buscar información sobre los bloques de IP para los distintos países o continentes

## Ejercicio 4.8
### Buscar información sobre métodos y herramientas para implementar GSLB.

----------------------------------------------------------------------
# Tema5

## Ejercicio 5.1
### Buscar información sobre cómo calcular el número de conexiones por segundo.

## Ejercicio 5.2
### Revisar los análisis de tráfico que se ofrecen en: http://bit.ly/1g0dkKj Instalar wireshark y observar cómo fluye el tráfico de red en uno de los servidores web mientras se le hacen peticiones HTTP… o en la red de casa

## Ejercicio 5.3 
### Buscar información sobre características, funcionalidad, disponibilidad para diversos SO, etc de herramientas para monitorizar las prestaciones de un servidor.

- top
- vmstat
- netstat

----------------------------------------------------------------------
# Tema6

## Ejercicio 6.1 
### dfd
----------------------------------------------------------------------