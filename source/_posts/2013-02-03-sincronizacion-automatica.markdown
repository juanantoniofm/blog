---
layout: post
title: "blogging comodo con Octopress"
date: 2013-02-03 04:17
comments: true
categories: automation, blogging, scripts, shell, git
---

Con la vida ocupada de hoy en dia, no podemos perder tiempo en tareas mecanicas o repetitititititititivas :P

con unos pequeños scripts, la ayuda de crontab y pericia linuxera, podemos evitarnos tener que hacer login
en ninguna web, para postear en nuestro blog.

Para ello, utilizaremos __git__ (en concreto __[github](www.github.com)__ , __bash__, __markdown__, y un editor de texto, como __vim__.

Si no los conoces, 
- markdown, es un lenguaje de marcado, sencillo y facil de aprender, orientado a la redaccion de webs, pero con el puedes elaborar documentos presentables sin preocuparte con el estilo.

- git, es un sistema de control de versiones, usado por ejemplo para desarrollar el kernel de linux

- github, es un servicio de repositorios git gratuito. Hay muchos otros como bitbucket, pero hemos elegido github por su especial vinculacion con Octopress

- bash, es un interprete de comandos. Si no lo conoces, deja de leer e instala debian ;)


## Conociendo Octopress

Octopress es una plataforma de blogging que funciona de una manera especial. En lugar de servir paginas dinamicas con PHP como muchos otros, sirve paginas estaticas. punto. Sin problemas de seguridad, sin problemas de actualizaciones, y sin (casi) problemas de carga (necesita muchiiiiiisima menos potencia en el servidor que un blog con PHP+MySQL, por ejemplo.

Cada vez que escribes un articulo, hay que regenerar el sitio "entero". Para hacer todo esto comodamente, Octopress utiliza una serie de "tareas" de ruby (rake).

Por un lado, se instala el Octopress propiamente dicho, que contiene el codigo fuente, las tareas, etc
Por otro lado, tendremos el sitio con las paginas a publicar, el blog en si. Para publicar las paginas, podemos utilizar las paginas de github, [Heroku](http://www.heroku.com), o como es mi caso, tu propio servidor web.

La opcion mas natural para utilizarlo, es instalarlo en local, y cuando escribes un articulo, despliegas en el servidor. Pero este caso es especial :) 

Vamos a ir un poco mas alla, y vamos a prepararlo todo para poder publicar desde cualquier sitio, y que automaticamente se despliegue en nuestro servidor. __automagicamente__ 


## Instalando Octopress

Primero, lo instalaremos en el servidor, como si fuera una instalacion normal.
No voy a detallar mucho la instalacion, teneis la documentacion oficial. 
Resumiendo rapidamente, tenemos que instalar ruby, descargar un par de cosillas, configurar el blog en un fichero .yaml, y pista

## Configurando la automatizacion

La automatizacion consta de varias partes. Por un lado una tarea de ruby se encargara de vigilar el directorio con los posts en espera de que algo cambie, para re-generar el sitio automaticamente.
Por otro, tendremos una tarea cron que descargara los posts de un repositorio en github, bitbucket, o similar, actualizando nuestra carpeta, provocando que la tarea de re-generar se lance.
Y finalmente, nos tendremos que acordar de subir nuestros posts al repositorio cuando acabemos de editarlos. Calma, tambien haremos un script para esto.

### Regenerando el sitio automaticamente

En la maquina en la que tenemos instalado Octopress, crearemos un demonio que ejecutara

	$ rake watch

La tarea que re-generara nuestro sitio.

### Sincronizando con el repositorio automaticamente _

En la misma maquina en la que hemos instalado Octopress, configuraremos una tarea Cron para que actualice nuestra carpeta de posts.

Bastara con editar un archivo de texto, _sincroniza-blog.sh_, con algo como esto:

	{% codeblock lang:bash %}
	#!/bin/bash
	cd /ruta/a/la/instalacion/de/octopress
	git pull
	{% endcodeblock %}

y luego darle permisos de ejecucion y moverlo a la carpeta correspondiente de crontab

	$ sudo su -                                # entrar como root
	% mv sincroniza-blog.sh /etc/cron.hourly   # mover el script
	% chown root:root sincroniza-blog.sh       # cambiar el owner
	% chmod +x sincroniza-blog.sh              # dar permisos de ejecucion
	% exit                                     # Para salir de la sesion de root 

De esta forma, se ejecutara automaticamente cada hora.

### Facilitando la publicacion

Y como buen programador (e incluso te diria algun buen lenguaje de programacion) tenemos que ahorrar golpes de teclado (no confundir con vagancia ;) 
Y utilizaremos de nuevo otro script bash. NOTA: aseguraros de haber ejecutado un git _push origin master_ al menos antes d lanzar este script.

	{%codeblock lang:shell %}
	#!/bin/bash
	cd /ruta/al/repo/del/blog
	git commit -a
	git push

## Escribiendo el primer post (y siguientes ;)

Y con todo configurado, ya podemos ponernos manos a la obra. 
Entra en la carpeta \_posts y crea un nuevo post haciendo una copia de la plantilla

