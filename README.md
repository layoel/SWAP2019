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
	- [*Django*](https://hackernoon.com/top-10-python-web-frameworks-to-learn-in-2018-b2ebab969d1a): Es de código abierto, sus carácterísticas principales son su autenticación, el enrutamiento de URL, el mapeo de objetos relacionales y las migraciones del esquema de la base de datos. Usa su ORM para asiganr los objetos a tablas de la base de datos. El mismo código funciona con diferentes base de datos y no es dificil transferir datos de una base de datos a otra diferente. Trabaja con PostgreSQL, MySQL, SQLite y Oracle.
	- [*Pyramid*](https://hackernoon.com/top-10-python-web-frameworks-to-learn-in-2018-b2ebab969d1a): algunas de sus carácterísticas son generar aplicaciones de un solo archivo, generación de URL, la configuración es extensible, autenticación y autorización flexibles, ofrece pruebas, soporte y documentación completa.
	- [*web2py*](https://hackernoon.com/top-10-python-web-frameworks-to-learn-in-2018-b2ebab969d1a): No tiene requisitos minimos de instalación y configuración, puede ejecutarse en cualquier sistema operativo o en Google App Engine, Amazon EC2 y cualquier alojamiento web que admita python 2.5-2.7 o java. Implementa niveles altosd e seguridad apra prevenir vulnerabilidades como secuencias de comandos entre sitios, inyección de código o ejecución de archivos maliciosos. El código es fácil de leer y mantener. Lleva registro de errores y de accesos, control de acceso basado en roles con distintos permisos.
	- [*Flask*](https://hackernoon.com/top-10-python-web-frameworks-to-learn-in-2018-b2ebab969d1a): Sus características más útiles son que funciona como servidor de desarrollo y es rápido para depurar. Lleva integrado un soporte para pruebas. Soporte seguro de cookies. Está basado en Unicode. Te premite conectar cualquier ORM y maneja solicitudes HTTP. Licencia BSD.
	- [*Bottle*](https://hackernoon.com/top-10-python-web-frameworks-to-learn-in-2018-b2ebab969d1a): Se pensó originalmente para crear API, lo implementa todo en un solo archivo fuente. No tiene dependencias aparte de la biblioteca estandar de python. Sus características principales incluyen enrutamiento, plantillas, utilidades y una abstracción básica sobre el estandar WSGI.
	- [*Tornado*](https://hackernoon.com/top-10-python-web-frameworks-to-learn-in-2018-b2ebab969d1a):Usa una red de Entrada/salida no bloqueante y puede manejar mas de 10.000 conexiones simultáneas correctamente. Sus características principales son: servicios en tiempo real, rendimiento de alta calidad, lenguaje de plantillas web basado en python, cliente HTTP sin bloqueo entre otras.
- [Frameworks para web con java](https://openwebinars.net/blog/los-7-mejores-frameworks-de-java/):
	- [*Spring MVC*](https://openwebinars.net/blog/los-7-mejores-frameworks-de-java/): Ofrece una amplia gama e servicios como son API REST, servicios web SOAP, seguridad... Tiene una gran comunidad de desarrolladores que trabajan con el y tiene una documentación muy buena. Es una herramienta muy poderosa para el desarrollo de aplicaciones web y de proyectos de seguridad.
	- [*Struts 2*](https://openwebinars.net/blog/los-7-mejores-frameworks-de-java/): Tiene un conjunto de herramientas para crear aplicaciones web orientadas a epmresas que optimizan el proceso de desarrollo de principio a fin y el mantenimiento posterior.
	- [*Hibernate*](https://openwebinars.net/blog/los-7-mejores-frameworks-de-java/): Las características de este software ayudan a los desarrolladores back-end a acceder a los datos. Este framework permite realiar opreaciones en la base de datos de objetos Java.
	- [*Goggle Web Toolkit*](https://openwebinars.net/blog/los-7-mejores-frameworks-de-java/): Permite a los programadores crear y optimizar sofisticadas aplicaciones basadas en la web . El kit de desarrollo de software GWT ofrece APIs Java y widgets básicos para la construcción de aplicaciones compiladas después de aplicarles JavaScript.
	- [*Grails*](https://openwebinars.net/blog/los-7-mejores-frameworks-de-java/):  es considerado como una herramienta dinámica que mejora la productividad de los ingenieros debido a sus APIs, a sus valoress por defecto. Tiene un conjunto de herramientas poderosas, tales como la inyección de dependencia Spring-powered y diversos complementos, que ofrecen todo lo necesario para crear modernas aplicaciones web.

## Ejercicio 2.3
### ¿Cómo analizar el nivel de carga de cada uno de los subsistemas en el servidor? Buscar herramientas y aprender a usarlas. ...¡o recordar cómo usarlas!

- [Monitorización de servidor linux por consola](https://openwebinars.net/blog/3-formas-de-monitorizar-servidores-linux/)
	- [top](https://linux.die.net/man/1/top):**Top, htop** y **dstat** permiten visualizar la carga de cpu, el uso de memoria, la informacion de procesos etc.
	- [htop](https://linux.die.net/man/1/htop)
	- [dstat](https://linux.die.net/man/1/dstat)
	- [ps](http://linuxcommand.org/lc3_man_pages/ps1.html): muestra información detallada de los procesos de sistema, se puede filtrar por suuarios y detalles de los procesos.Las opciones mas usuales de utilizar pueden ser aux o fax , indicando la opción a junto con x para incluir todos los procesos, y las opciones f y u que se utilizan para seleccionar la visualización en árbol o detallada, respectivamente.
	- [lsof](https://linux.die.net/man/8/lsof): permite mostrar los ficheros abiertos asociados tanto a procesos como a servicios (sockets, tuberías, etc). Si ejecutamos lsof sobre un fichero o directorio, podremos ver si éste esta siendo ocupado por algún proceso.
	- [netstat](https://linux.die.net/man/8/netstat): herramienta para monitorizar el estado de nuestra red. Para saber el estado de las conexiones.
	- [route](https://linux.die.net/man/8/route): herramienta para monitorizar el estado de nuestra red. Para analizar las tablas de rutas.
	- [iptraf](https://linux.die.net/man/8/iptraf): herramienta para monitorizar el estado de nuestra red.
	- [iftop](https://linux.die.net/man/8/iftop): herramienta para monitorizar el estado de nuestra red.
	- [df](https://linux.die.net/man/1/df):  Para visualizar el uso del disco.
	- [iotop](https://linux.die.net/man/1/iotop): Si lo que queremos visualizar es el I/O del disco, este comando nos muestra los procesos del sistema y su trabajo de interrupción en el disco.

- [Monitorización de un servidor Linux: Aplicaciones de interfaz web](https://openwebinars.net/blog/3-formas-de-monitorizar-servidores-linux/)
	- [cacti](https://hipertextual.com/archivo/2010/09/monitoriza-el-estado-de-tu-red-con-cacti/): permite monitorizar y visualizar gráficas y estadísticas de dispositivos conectados a una red y que tengan habilitado el protocolo SNMP, ya sea un switch, un router o un servidor Linux.
	- [munin](https://www.ecured.cu/Sistema_de_monitoreo_Munin) : Es una herramienta multiplataforma basada en web, utilizada en el monitoreo de los recursos en red. Permite monitorizar muchos parámetros y visualizarlos en cómodas gráficas. Toda la información generada puede verse a través de la web desde cualquier parte. Está implementado en Perl y liberado bajo licencia GPL.
	- [collectd](https://www.elarraydejota.com/monitorizando-el-sistema-con-collectdinfluxdbgrafana-debian/): Es un servicio que recolecta datos del sistema operativo y de las aplicaciones, generando métricas periódicas y suministrando mecanismos para almacenar dichos datos, en registros o arrays.
- [Monitorización de infraestructuras](https://openwebinars.net/blog/3-formas-de-monitorizar-servidores-linux/)
	- Nagios
	- Zabix

	Ambas nos permiten controlar tanto los servicios de red como los recursos hardware de los equipos, pudiendo ampliar dichas funcionalidades gracias a plugins y scripts proporcionados por nosotros. Tienen sistemas de alertas que nos permiten indicar varios niveles de alerta a diferentes medios dependiendo del tiempo que pase la incidencia activa, así como programar acciones para intentar solventar la incidencia de forma automática.

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