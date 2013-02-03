---
layout: post
title: "mosh mejora ssh"
date: 2012-10-17 18:39
comments: true
categories: sysadmin, linux, cli
---

_Tiempo de lectura estimado: **2 minutos 22 segundos **_

SSH lleva muchos años entre nosotros, y es insustituible, pero mejorable. **Mosh complementa a SSH** a la hora de administrar maquinas por consola, **sobre todo cuando tenemos una conexion pobre**, lenta, con interrupciones, o movil.

## Para instalar mosh

De entre la [Lista de clientes](http://mosh.mit.edu/#getting) podemos escoger para practicamente cualquiera de nuestras plataformas, aunque si lo quieres usar en windows, tendras que instalar Cygwin (jejeje) 



### en Debian

Con los repos de squeeze-backports habilitados, basta con un 

		
		$ sudo apt-get install mosh
		

### En RHEL / CentOS
Para instalar mosh en un servidor basado en redhat, tendremos que utilizar los [repositorios de EPEL](http://fedoraproject.org/wiki/EPEL).
Ojo, hay que tener mucho cuidado y no mezclar repos orientados a Fedora, con los orientados a CentOS. [Aqui](http://wiki.centos.org/AdditionalResources/Repositories) puedes ver "What NOT to do". Echale un vistazo (son dos parrafos), y evita males mayores.

Despues, bastara con 

		$ sudo yum install mosh

Y alegria!

### En Android 
Para usar en un cacharro con android (habitualmente un telefono) tenemos disponible un [port construido sobre el cliente IRSSI ConnectBot](http://dan.drown.org/android/mosh/), que algunos ya conocereis.
Instalarlo es muy facil, basta con [Descargar la version modificada](http://dan.drown.org/android/mosh/irssiconnectbot-release.apk) de ConnectBot 

### A pelo como los paisanos
Siempre podremos compilar la veresion de codigo fuente, si no encontramos una opcion que surta a nuestra  distro.
Para compilarla, hay dos opciones, Cogiendo la version de GitHub, o [descargando el paquete](https://github.com/downloads/keithw/mosh/mosh-1.2.2.tar.gz).

#### Para conseguirla de GitHub

Clona el repositorio y lanza el autogen

		$ git clone https://github.com/keithw/mosh
		$ cd mosh
		$ ./autogen.sh

#### Para instalar el codigo fuente

Tanto si has descargado el paquete y lo tienes descomprimido en una carpeta, como si descargaste el repo y lanzaste el autogen, solo tendras que seguir los pasos tipicos de instalacion.

		$ ./configure
		$ make
		# make install


