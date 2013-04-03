---
layout: post
title: "Monitorizacion de aplicaciones web para benchmarking"
date: 2013-03-13 04:19
comments: true
categories: sysadmin, benchmarking, loadtest, monitoring, monitorizacion, pruebas de carga
---

Cuando monitorizamon una aplicacion o un sistema con el objetivo de encontrar los cuellos de botella que afectan a su rendimiento, tenemos unas necesidades de monitorizacion especiales, que no todas las herramientas poseen. En este articulo, hago una criba en base a mi experiencia, separandolas entre herramientas graficas (que te dejan un precioso dibujin) y las que no (aunque luego puedas perfectamente transformar los datos en preciosas graficas).


## Aplicaciones con graficos

La mayoria estan basadas en una interfaz web. Algunas como munin o nagios, no nos sirven, ya que su intervalo de actualizacion suele ser bajo, y su montaje un tanto complejo para simplemente estresar una aplicacion web.

### Java Melody

Una pequeña aplicacion, que se instala en el servidor de aplicaciones (ojo que no todos estan soportados) y nos muestra detalles de lo que esta pasando por dentro de nuestra pequeña aplicacion. Desde que el usuario entra hasta que sale. Por suerte, esta aplicacion no introduce mucha instrumentacion en nuestro codigo, y [no supone ninguna gran perdida de rendimiento] (https://groups.google.com/forum/?fromgroups=#!topic/javamelody/39txASF__Lw).

Las graficas se elaboran con los datos unicamente estadisticos que recoge (una de las claves de su bajo impacto es que no guarda demasiados detalles, al fin y al cabo solo necesitamos estadisticas). Estan hechas con rddtool, asi que a mas de uno le resultara familiar el estilo. [Aqui se pueden ver algunas capturas de pantalla](http://code.google.com/p/javamelody/wiki/Screenshots)
![JavaMelody captura de pantalla de las graficas](http://javamelody.googlecode.com/svn/trunk/javamelody-core/src/site/resources/screenshots/graphs.png "Captura de pantalla de las graficas de javamelody")
[Instalacion de JavaMelody[(http://blog.klicap.es/archives/175)

### VisualVM & JConsole

Mientras que el primero se mantiene fiel a las formas clasicas, es ligero y relativamente facil de conectar, VisualVM o jvisualvm llega ser mas que un profiler de java, extendiendolo a traves de plugins, como el GCPlugin que nos muestra informacion detallada de como esta recogiendo la basura nuestra querida JVM.

Conectar estas herramientas con un Tomcat o un Jboss es sencillo, aunque cuando hay problemas cuesta averiguar el porque. A veces hay que tener consideraciones especiales, segun el servidor de aplicaciones que utilicemos, como con Jboss AS 7: [Como conectar VisualVM a Jboss7](http://juanantonio.fm/xxxxxxxxxxxxxxxxxxxxx) 

## Aplicaciones de consola para monitorizar aplicaciones Java

En un precioso nuevo articulo, que este se hace pesado :D
Hablaremos de iostat, iotop, sar, vmstat, iptraf y dstat
y para mirar la coleccion de basura, habilitamos las opciones _ -Xloggc:<file> -XX:+PrintGCDetails_, miramos el log, y lo parseamos con [GCViewer](http://www.tagtraum.com/gcviewer.html)
