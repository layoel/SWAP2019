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

- Balanceadores de carga software:
	- [Brocade](https://gigas.com/balanceador.html): 
		-Entrega de Aplicaciones y solución de Balanceador de Carga diseñados especialmente para la Virtualización de Funciones de Red de alto rendimiento (NFV)
		- Balanceo de carga inteligente
		- Aceleración de aplicaciones
		- Almacenamiento en caché de contenido dinámico
		- Descarga SSL y de compresión
		- Monitorización de nivel de servicio
		- Balanceo de carga global
		- Gestión de ancho de banda
		- Automatización de servicio utilizando REST API
		- Appliance NFV para la entrega de aplicaciones 
	- [Zevenet](https://www.zevenet.com/) (visto en clase)
	- [Haproxy](https://www.redeszone.net/2014/10/25/haproxy-un-balanceador-de-cargas-tcphttp-gratuito/) (visto en clase)
	- [Nginx](https://picodotdev.github.io/blog-bitix/2016/07/configurar-nginx-como-balanceador-de-carga/) (visto en clase)
	- [Pound](https://linuxtechlab.com/load-balancing-web-servers-using-pound-load-balancer/) (hecha práctica opcional en la práctica de balanceadores)
	- [Pen](http://blog.capacityacademy.com/2014/06/17/montando-balanceador-de-carga-en-linux-centos/): es una balanceador de carga simple que nos permitirá tener varios servidores en línea proveyendo un servicio y que aparezcan como uno públicamente. Es capaz de detectar los servidores que no están disponibles y distribuir la carga entre los que están, dándonos alta disponibilidad y rendimiento escalable. Cuenta con varias características y podemos implementarlo en una máquina virtual o en una maquina sin muchos recursos reduciendo el costo de implementación.

- Balanceadores de carga hardware:
	- [Barracuda](https://www.barracuda.com/products/loadbalancer): solución Enterprise Ready a un muy buen precio.  Ideal para optimizar el rendimiento de las aplicaciones. Libera al servidor de transacciones SSL que consumen muchos recursos, lo que permite conservar recursos para las aplicaciones. Además, las funciones de optimización como el almacenamiento en caché, la compresión y la agrupación de TCP permiten una entrega de aplicaciones más rápida y garantizan la flexibilidad. Además de las funcionalidades estándar incluye prevención de intrusiones IPS, no IDS.
	- [F5](https://f5.com/glossary/load-balancing-101): Los F5 BIG-IP Load Traffic Manager (LTM), son otro de los clásicos en el mundo del balanceo de carga. Fáciles de usar y optimizados para trabajar sobre la WAN.
	- [CISCO](https://www.ovh.com/world/dedicated-servers/ace_load_balancing.xml) 
		- Tráfico de balanceo de carga en HTTP, FTP, DNS, SIP, RTSP, POP / IMAP, etc.
		- Tráfico SSL.
		- Permite asignar pesos para cada uno de sus servidores o VM
		- Configurar sensores de monitoreo
		- Gestión de NAT / DNAT para el rack virtual
		- Ver rendimiento con SNMP.

### Buscar productos comerciales para servidores de aplicaciones.

- Servidores de aplicaciones: 
	- [Apache Tomcat](https://www.charliejsanchez.com/2018/03/04/balanceadores-de-carga-con-haproxy-apache2-y-nginx/): ofrece una implementación libre de Java Servlet, JavaServer Pages, Java WebSocket, etc. para poder crear un servidor de aplicaciones, tanto para Windows como para Linux.
	- [ Microsoft Internet Information Services (IIS)](https://www.ibm.com/support/knowledgecenter/es/SSAW57_9.0.0/com.ibm.websphere.nd.multiplatform.doc/ae/tins_manualWebIIS.html)
	- [IBM WebSphere Application Server](https://www.ibm.com/support/knowledgecenter/es/ssw_ibm_i_73/rzahg/rzahgebappserv.htm):  es la implementación por parte de IBM de la plataforma Java Platform, Enterprise Edition (Java EE). WebSphere Application Server está disponible en paquetes exclusivos que están diseñados para cumplir una amplia gama de requisitos de cliente. En el centro de cada paquete hay un WebSphere Application Server que proporciona el entorno de ejecución para aplicaciones empresariales.
	- [Oracle IAS](https://www.adictosaltrabajo.com/2006/06/02/ias/): un sistema integrado, basado en los estándares software como plataforma.  Implementa aplicaciones basadas en Java EE. 
	- [Borland AppServer](https://www.computerweekly.com/feature/Borland-AppServer-45): es una implementación de alto rendimiento de un servidor de aplicaciones compatible con Java 2 Enterprise Edition (J2EE). Es uno de los primeros productos que han pasado el proceso de certificación J2EE de Sun.

### Buscar productos comerciales para servidores de almacenamiento.

- [Servidores de almacenamiento](https://www.xataka.com/otros-dispositivos/guia-de-compra-de-nas-multimedia-en-que-debes-fijarte-y-cuales-son-los-mejores-modelos):
	- [NAS](https://gouforit.com/10-mejores-servidores-nas/)
		- Sygnology
		- Qnap
		- Western Digital
		- Netgear
		- D-link
		- iomega
	- [SAN](https://www.netapp.com/es/info/what-is-storage-area-network.aspx): Las siglas SAN significan Storage Area Network, en español significan redes de área de almacenamiento. Ésta es la arquitectura de redes de almacenamiento más común que utilizan las empresas para que sus aplicaciones más relevantes alcancen un alto rendimiento y una baja latencia. Un almacenamiento SAN se basa en bloques y saca partido de una arquitectura de alta velocidad que conecta los servidores con sus unidades de disco lógicas (LUN). Una LUN es una variedad de bloques que se aprovisionan desde un grupo de almacenamiento compartido y se presentan al servidor como un disco lógico. El servidor divide y da formato a esos bloques (por lo general, con un sistema de archivos) para que se puedan almacenar datos en la LUN igual que se haría en el disco local.
	- [DAS](https://espai.stucom.com/tecnologia/sistemas-de-almacenamiento-das-nas-san/): Almacenamiento directamente conectado. Es el tipo de almacenamiento tradicional. Un disco duro de un servidor, conectado a su placa base mediante una controladora de disco integrada es el ejemplo más representativo de un sistema DAS. El sistema operativo accede al almacenamiento mediante bloques, el sistema operativo es el encargado de poner en ese disco particiones y sistemas de ficheros, para poder almacenar carpetas u ficheros en él.
		- Infortrend
		- Chenbro

--------------------------------------------------------

# Tema3

## Ejercicio 3.1 
### Buscar con qué órdenes de terminal o herramientas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.

- [En windows](https://pcteando.wordpress.com/2014/01/23/configurar-windows-server-2008-como-router-y-nat/): Para windows server 2008 tendremos que agegar la funcion de "servicios de acceso y directiva de redes" y añadir "servicios de enrutamiento y acceso remoto", en windows todo se puede hacer desde el entorno gráfico, solo hay que darle a siguiente e instalar. Una vez instalada la herramienta, solo tenemos que pinchar encima de "enrutamiento y acceso remoto" y darle a configurar y habilitar, aquí habilitaremos la opción de "traducción de direcciones de red NAT", seleccionamos la interfaz de red que hará de puerta de enlace y configuraremos la ip, la mascara de subred, la puerta de enlace y los DNS. En el resto de equipos tendremos que poner como puerta de enlace la ip de nuestro windows server para que sea el que haga el NAT.
- [En Linux](http://www.vicente-navarro.com/blog/2011/10/07/accediendo-a-una-red-mediante-nat-en-linux/): En linux, el enrutamiento se puede hacer con iptables. Lo vamos a ver con un ejemplo, en el que tenemos un servidor que une la intranet con una red interna y queremos montar un NAT. Las tarjetas de red tienen del servidor tienen las IPs 10.25.25.2 la que conecta con la intranet y 172.16.20.2 la que conecta con la red interna.

Primero tenemos que permitir el IP Forwarding, para que pasen paquetes de un interfaz a otro.

```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```
Para que se aplique cada vez que reiniciemos tenemos que añadirlo al fichero */etc/sysctl.conf* esta linea

```bash
net.ipv4.ip_forward = 1
```

A continuación tendriamos que habilitar el NAT para que los nodos de la red oculta puedan acceder a los nodos de la intranet.

```bash
/sbin/iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

Tras ejecutarlo, ya todos los nodos de la red oculta podrán acceder a nodos de fuera.
Para permitir la comunicación en el sentido inverso, desde la intranet a la red oculta, tendríamos que hacer lo equivalente a cuando “abrimos puertos”

```bash
/sbin/iptables -A PREROUTING -t nat -p tcp -d 10.25.25.2 --dport 224 -m state --state NEW,ESTABLISHED,RELATED -j DNAT --to 172.16.20.4:22
```

Hacemos lo mismo con conexiones que lleguen a la IP 10.25.25.2 y puerto 225, que redirigimos “NATeadas” a la IP 172.16.20.5, puerto 22 (SSH):

```bash
/sbin/iptables -A PREROUTING -t nat -p tcp -d 10.25.25.2 --dport 225 -m state --state NEW,ESTABLISHED,RELATED -j DNAT --to 172.16.20.5:22
```

Lo mismo con conexiones que lleguen a la IP 10.25.25.2 y puerto 33896, que reenviamos a la IP 172.16.20.6, puerto 3389 para permitir el acceso remoto.

```bash
/sbin/iptables -A PREROUTING -t nat -p tcp -d 10.25.25.2 --dport 33896 -m state --state NEW,ESTABLISHED,RELATED -j DNAT --to 172.16.20.6:3389
```


## Ejercicio 3.2 

### Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.

- En linux: se usa iptables, no pongo ejemplos porque me remito a la práctica de este tema donde usamos iptables para bloquear o permitir paquetes desde ips concretas o de algun protocolo concreto o bloquear todo el tráfico etc.
- En windows: Se puede usar el firewall de windows. En [esta web](https://www.itprotoday.com/security/packet-filtering-and-windows) podemos ver las opciones que hay de filtrado.

----------------------------------------------------------------------
# Tema4

## Ejercicio 4.1

### Buscar información sobre cuánto costaría en la actualidad un mainframe que tuviera las mismas prestaciones que una granja web con balanceo de carga y 10 servidores finales (p.ej).

## Ejercicio 4.2

### Buscar información sobre precio y características de balanceadores comerciales (hardware) específicos. Compara las prestaciones que ofrecen unos y otros.

Uno de los Balanceadores Hardware de los que hablamos en clase es Barracuda, así que he buscado información en la web oficial del fabricante y nos deja comparar de 4 en 4 sus servidores y las características. En [esté enlace](https://www.barracuda.com/products/loadbalancer/models/compare/1?models=340,440,640,841) está la descripción y las características de los 4 que he seleccionado.

![imagen](https://github.com/layoel/SWAP2019/blob/master/imagenes-ejercicios/8.JPG)
![imagen](https://github.com/layoel/SWAP2019/blob/master/imagenes-ejercicios/9.JPG)
![imagen](https://github.com/layoel/SWAP2019/blob/master/imagenes-ejercicios/10.JPG)
![imagen](https://github.com/layoel/SWAP2019/blob/master/imagenes-ejercicios/11.JPG)

El precio no aparece en su propia web pero buscando en otras web he encontrado los siguientes precios:

- [Barracuda Load Balancer 240](https://www.cnet.com/products/barracuda-load-balancer-240-load-balancing-device-series/) $1,924.49
- [Barracuda Load Balancer ADC 440](https://www.cnet.com/products/barracuda-load-balancer-440-load-balancing-device-series/) $5,451.66
- [Barracuda Load Balancer ADC 540](https://www.zones.com/site/product/index.html?id=101081443) $8,000.99
- [Barracuda Load Balancer ADC 640](https://www.firewalls.com/products/wan-accelerator/barracuda-load-balancer/640) $10,971.46
- [Barracuda Load Balancer ADC 841](https://www.zones.com/site/product/index.html?id=101081443) $8,000.99
- [Barracuda Load Balancer ADC 841](https://www.barraguard.co.uk/840-ADC-10GbE-Copper.asp) £22,867.90

## Ejercicio 4.3

### Instala y configura en una máquina virtual el balanceador ZenLoadBalancer. Compara con la dificultad de la instalación y configuración usando nginx o haproxy (práctica 3).

Primero descargo la imagen de [aqui](https://osdn.net/projects/zevenet/storage/zevenet-ce_v5.9.1-amd64.iso/)

Para la instalación he seguido la [guia de instalación oficial](https://www.zevenet.com/es/base-de-conocimientos/Edici%C3%B3n-de-Empresa/Gu%C3%ADa-de-administraci%C3%B3n-de-la-edici%C3%B3n-empresarial-v3-04/Edici%C3%B3n-de-la-empresa-v3-04-gu%C3%ADa-de-instalaci%C3%B3n/)

La instalación es sencilla

![imagen](https://github.com/layoel/SWAP2019/blob/master/imagenes-ejercicios/1.JPG)

nos pide una dirección ip para nuestro balanceador, la mascara, la puerta de enlace y la dirección del servidor dns.

![imagen](https://github.com/layoel/SWAP2019/blob/master/imagenes-ejercicios/2.JPG)

A continuación pide un nombre para el equipo y un nombre de dominio.

![imagen](https://github.com/layoel/SWAP2019/blob/master/imagenes-ejercicios/3.JPG)

Seguimos con el particionamiento del disco y una vez terminado comienza la instalación

![imagen](https://github.com/layoel/SWAP2019/blob/master/imagenes-ejercicios/4.JPG)

Una vez terminada la instalación iniciamos el sistema sin el disco de instalación. El usuario es root y la contraseña la que pusimos en la instalación

![imagen](https://github.com/layoel/SWAP2019/blob/master/imagenes-ejercicios/5.JPG)

Para acceder a la configuración desde otra máquina podemos acceder a la web **https://192.168.80.15:444** donde nos pedira usuario y contraseña que es el mismo que en el apartado anterior

![imagen](https://github.com/layoel/SWAP2019/blob/master/imagenes-ejercicios/6.JPG)

Una vez hemos accedido al interfaz web, es facil crear una granjaweb desde el apartado LSLB - Farms la creamos y en ese menu añadimos un nuevo servicio que llamamos web y en add backend añadimos las ips y los puertos de los servidores web que vamos a balancear.

![imagen](https://github.com/layoel/SWAP2019/blob/master/imagenes-ejercicios/7.JPG)

Si comparamos la configuración con la que hicimos en nginx en haproxy o en pound la verdad la de zevenet al ser por web es más intuitiva, más comodo y menos propensa a errores en la configuración bajo mi punto de vista.


## Ejercicio 4.4

### Buscar información sobre los métodos de balanceo que implementan los dispositivos recogidos en el ejercicio 4.2 (o el software que hemos propuesto para la práctica 3).

Los métodos de balanceo del software de la práctica 3 para **[Nginx](http://nginx.org/en/docs/http/load_balancing.html)** son:

- *Round Robin*: una petición por cada servidor. Se suele usar cuando todos los equipos que montan la web son de identicas características, para que ninguno de los servidores esté sobrecargado y todos tarden lo mismo en responder a los clientes.
- *IP Hash*: crea un hash de la direccion ip, con los 3 primeros bytes de la IP. Esa función hash se usa para determinar que servidor debe seleccionar para la siguiente solicitud dependiendo de la IP del cliente que realiza la petición.
- *Menos conectado*: el servidor que ha tenido menos conexiones activas es al servidor al que va a mandar la petición nueva.


## Ejercicio 4.5 

### Probar las diferentes maneras de redirección HTTP. ¿Cuál es adecuada y cuál no lo es para hacer balanceo de carga global? ¿Por qué?

Los [códigos de estado http](https://diego.com.es/redirecciones-http) para redirecciones está regulados en el RFC7231. 

- **300 multiple choices**
- **301 moved permanently**
- **302 found**
- **303 see other**
- **307 temporary redirect**
- **308 permanent redirect**

En la imagen siguiente podemos ver un resumen de los códigos anteriores.

![Imagen](https://github.com/layoel/SWAP2019/blob/master/GranjaWebDocker/imagenes/35.JPG)

Yo creo que los que se pueden usar para GSLB son el 301,307 y 308 porque te permiten redirigir a otra web.

## Ejercicio 4.6 

### Buscar información sobre los bloques de IP para los distintos países o continentes

He encontrado una página donde ordena las ips por paises. Es [esta](https://lite.ip2location.com/ip-address-ranges-by-country) si entras dentro de cada país obtienes el listado de direcciones ip y al final de ese listado te aparece para que puedas descargarlo en CSV por si necesitas que la información esté accesible para trabajar con ella. En [esta](https://www.xmyip.com/ip-blocks-countries) otra web al acceder nos da un poco mas de información que en la web anterior, señala los rangos y el estado o región al que está asignado incluso hay una columna para la ciudad.

## Ejercicio 4.7

### Buscar información sobre métodos y herramientas para implementar GSLB.

Para implemenar un GSLB necesitamos tener nuestro centro de datos replicado en dos localizaciones distintas, sino no tiene sentido usar un GSLB. Partiendo de esa base, el propio Zevenet nos da la posibilidad de implementar un GSLB en [esta web](https://www.zevenet.com/es/base-de-conocimientos/howtos/c%C3%B3mo-funciona-el-servicio-global-de-equilibrio-de-carga-gslb/) explican detalladamente como hacerlo. Otra opción es usar el GSLB NetScaler de Citrix XenMobile aquí nos [explican como funciona y la configuración](https://docs.citrix.com/es-es/xenmobile/server/advanced-concepts/xenmobile-deployment/disaster-recovery.html). La plataforma Amazon Web Services también tiene su propio GSLB, es Elastic Load Balancing, en [esta web](https://docs.aws.amazon.com/es_es/codedeploy/latest/userguide/deployment-groups-create-load-balancer.html) explican la configuración.


----------------------------------------------------------------------
# Tema5

## Ejercicio 5.1

### Buscar información sobre cómo calcular el número de conexiones por segundo.

Nginx nos da la posibilidad de realizar estadísticas que incluyen las conexiones de la máquina.Solo hay que añadir al fichero de configuración lo siguiente:

```BASH
location /nginx_status {
	# Para activar las estadísticas
	stub_status on;
	access_log   off;

	allow 192.168.80.133;
	deny all;
}

```

Para que se aplique, debemos reiniciar el servicio, como ocurre con cualquier cambio que hagamos sobre el fichero de configuración de nginx.

```bash
elvira@LB:~$ sudo service nginx restart
```

Para poder acceder a las estadísticas de nuestro sitio web, en el navegador debemos poner la ip de nuestro sitio y acontinuacion **nginx_status**
```bash
http://192.168.80.133/nginx_status
```

Para los servidores web que no usan nginx se puede hacer con el comando netstat y filtrando con grep. Por ejemplo:

```bash
#vemos todas las coneziones activas al servidor web
$ netstat -na

# Si queremos saber todas las conexxiones http filtramos asi:
$ netstat | grep -c http | wc -l 

# Para ver las conexiones activas en el puerto 80
$ netstat | grep :80
```
## Ejercicio 5.2

### Revisar los análisis de tráfico que se ofrecen en: http://bit.ly/1g0dkKj Instalar wireshark y observar cómo fluye el tráfico de red en uno de los servidores web mientras se le hacen peticiones HTTP… o en la red de casa

No pongo capturas de la instalación de wireshark porque ya lo tenia instalado en el equipo. 

Lo que he hecho ha sido filtrar solo la tarjeta wireless para capturar el tráfico wifi en la red de mi casa pero he aplicado un filtro para ver solo las peticiones http y este es el resultado obtenido.

![imagen](https://github.com/layoel/SWAP2019/blob/master/imagenes-ejercicios/12.JPG)

## Ejercicio 5.3 

### Buscar información sobre características, funcionalidad, disponibilidad para diversos SO, etc de herramientas para monitorizar las prestaciones de un servidor.

-  [top](https://linux.die.net/man/1/top):**Top, htop** y **dstat** permiten visualizar la carga de cpu, el uso de memoria, la informacion de procesos etc.
- [vmstat](https://www.solvetic.com/tutoriales/article/6174-como-usar-comando-vmstat-linux/): La herramienta vmstat ha sido desarrollada con el fin de brindar información a los administradores sobre procesos, memoria, paginación, E/S de bloque, actividad de la CPU, número de cambios de contexto, interrupciones de dispositivo y llamadas del sistema con el fin de acceder a los mejores detalles de control.
- [netstat](https://www.nerion.es/soporte/tutoriales/entendiendo-el-manejo-de-netstat/): Es una utilidad para conocer las conexiones establecidas entre nuestro PC y el exterior. Permite  entre varias cosas conocer la actividad de nuestra red, nos muestra que puertos de nuestro PC (netstat puertos), se encuentran abiertos y si son usados en alguna conexión desconocida. Permitiéndonos cerrarlos, si no los necesitamos.

----------------------------------------------------------------------
# Tema6

## Ejercicio 6.1 
### Aplicar con iptables una política de denegar todo el tráfico en una de las máquinas de prácticas. Comprobar el funcionamiento.

Este ejercicio lo realicé en la práctica 4:

Primero **bloqueando todo el tráfico**.

```bash
elvira@:~m1$ sudo iptables -P INPUT DROP 
elvira@:~m1$ sudo iptables -P OUTPUT DROP
elvira@:~m1$ sudo iptables -P FORWARD DROP
```
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/12.JPG)

### Aplicar con iptables una política de permitir todo el tráfico en una de las máquinas de prácticas. Comprobar el funcionamiento.

Para aceptar todo el tráfico, añadimos las siguientes reglas de iptables, antes debemos borrar las de bloquear todo:

```bash
elvira@:~m1$ iptables -F
elvira@:~m1$ iptables -X
elvira@:~m1$ iptables -Z
elvira@:~m1$ iptables -t nat -F
elvira@:~m1$ iptables −P INPUT ACCEPT
elvira@:~m1$ iptables −P OUTPUT ACCEPT
elvira@:~m1$ iptables −P FORWARD ACCEPT
```
![imagen](https://github.com/layoel/SWAP2019/blob/master/PRACTICAS/Practica4/imagenes/13.JPG)
## Ejercicio 6.2 
### Comprobar qué puertos tienen abiertos nuestras máquinas, su estado, y qué programa o demonio lo ocupa.

## Ejercicio 6.3 
### Buscar información acerca de los tipos de ataques más comunes en servidores web (p.ej. secuestros de sesión). Detallar en qué consisten, y cómo se pueden evitar.


----------------------------------------------------------------------
# Tema7

## Ejercicio 7.1 
### Buscar información sobre los sistemas de ficheros en red más utilizados en la actualidad y comparar sus características. Hacer una lista de ventajas e inconvenientes de todos ellos, así como grandes sistemas en los que se utilicen.
----------------------------------------------------------------------