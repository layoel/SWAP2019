# EJERCICIOS DE SWAP 2019

# Tema1

## Ejercicio 1.1 **Buscar información sobre las tareas o servicios web para los que se usan más los programas:**

- **Apache**: La wikipedia define " Apache es un servidor web HTTP de código abierto, para plataformas Unix (BSD, GNU/Linux, etc.)" La web oficial de [Apache](https://httpd.apache.org/) podemos encontrar  toda la documentación necesaria para instalar y configurar un servidor con Apache. Si indagamos un poco por la red podemos ver que algunas empresas importantes que usan apache incluyen a Cisco, IBM, Salesforce, General Elecctric Adobe, VMWare, Xerox, Linkedln, Facebook, Hewlett-Packard, At & T, Siemens, Ebay y más.[fuente](https://kinsta.com/es/base-de-conocimiento/que-es-apache/). 

- **Nginx**: También es un servidor web de código abierto, ahora también es usado como proxy inverso, caché de HTTP y balanceador de carga. La versión mas actual de Nginx es la 3.1 Mejora las funcionalidades de apache por ejemplo para sitios web estáticos o sitios web con alto tráfico. La web oficial de [nginx](https://www.nginx.com/). Originalmente fue creado por Igor Sysoev y apareció en público en octubre de 2004. Es una opción Opensource de alto rendimiento, muy ligera y flexible. Su característica principal es la asincronía. Nginx mejora el rendimiento de webs con respecto a Apache en cuanto a concurrencia, dado que es capaz de administrar más accesos concurentes de lo que lo podría hacer Apache y empleando menores requisitos de memoria.

- **thttpd**: Su [web oficial](http://acme.com/) nos dice que es un servidor web de código libre disponible para la mayoría de versiones unix. Sus características principales son que es simple, pequeño, portatil, rápido y seguro ya que utiliza los requerimientos mínimos de un servidor HTTP. Por ese motivo es ideal para servir grandes volúmenes de datos de información estática.[fuente](https://es.wikipedia.org/wiki/Thttpd) Podemos acceder a todas las opciones de configuración en el manual de linux [*man page thttpd(8)*](https://linux.die.net/man/8/thttpd) Los desarrolladores de este servidor son ACME Laboratories.

- **Cherokee**: En la [web oficial](http://cherokee-project.com/) nos definen cherokee como un servidor web de código abierto, innovador, rico en funciones, increiblemente rápido y fácil de configurar, diseñado para aplicaciones web seguras altamente concurrentes. Su configuración se hace a través de una interfaz web y nos dicen que es compatible con tecnologías como FastCGI,SCGI, PHP, uWSGI, SSI, CGI, LDAP, TLS/SSL, proxy HTTP, transmisión de vídeo, almacenamiento en caché de contenidos, configuración de tráfico... etc. Se puede ejecutar en Linux, MAC OS X, Solaris y BSD.

- **node.js**:La [web oficial de nodejs](https://nodejs.org/en/docs/guides/getting-started-guide/) nos dice que Node está diseñado para crear aplicaciones de red escalables. Nos permite manejar muchas conexiones al mismo tiempo. Una característica importante de Node es que no existen bloqueos porque casi ninguna funcion en Node se realiza sobre entrada/salida. Esto hace que sea el servidor web ideal cuando necesitamos escalabilidad. Node.js funciona en javascript, por lo que podemos usar este mismo lenguaje en el frontend y en el backend.

--------------------------------------------------------

# Tema2

## Ejercicio 2.1 **Calcular la disponibilidad del sistema si tenemos dos réplicas de cada elemento (en total 3 elementos en cada subsistema).**

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

## Ejercicio 2.2 **Buscar frameworks y librerías para diferentes lenguajes que permitan hacer aplicaciones altamente disponibles con relativa facilidad. Como ejemplo, examina PM2 [*https://github.com/Unitech/pm2* ](https://github.com/Unitech/pm2) que sirve para administrar clústeres de NodeJS.**

- [Frameworks para desarrollo web](https://www.wearemarketing.com/es/blog/frameworks-en-el-desarrollo-web-las-mejores-practicas-para-tu-negocio-online.html#):
~*Symfony 4* :Es el preferido por muchos desarrolladores web. Está compuesto por componentes que se pueden reutilizar y tiene una comunidad activa que expone nuevos códigos para el desarrollo de mejoras en actualizaciones. Tiene licencia libre, te da la capacidad de controlar accesos a la informacion, permite la creación de app en distintos idiomas, la facilidad de uso de su arquitectura y los diseños comprensibles y fáciles de usar para los desarrolladores web hacen que el código de este framework sea de calidad.~

*Laravel*
*CakePHP*
*CodeIgniter*
Frameworks para web con Python:
[*Django*]()
[*Pyramid*]()
[*web2py*]()
[*Flask*]()
[*Bottle*]()
[*web.py*]()
[Frameworks para web con java](https://openwebinars.net/blog/los-7-mejores-frameworks-de-java/):
*Spring MVC*:
*Struts 2*:
*Hibernate*:
*Vaadin*
*Goggle Web Toolkit*:
*Grails*:

----------------------------------------------------------------------