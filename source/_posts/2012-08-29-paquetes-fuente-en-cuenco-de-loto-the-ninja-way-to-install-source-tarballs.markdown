---
layout: post
title: "Paquetes Fuente en cuenco de loto - The ninja way to install source tarballs"
date: 2012-08-29 18:42
comments: true
categories: sysadmin, linux, tools
---

_Tiempo estimado de lectura: **3 minutos 49 segundos**_

Instalar desde el codigo fuente lo hace hasta un mono. La historia preocupante es ¿Quien lo desinstala?
No es que sea complicado o aburrido, es que es casi imposible hacerlo 100% bien. Siempre dejaras alguna libreria por algun lado, que puede llegar a costarte muy cara, en el momento en que entre en conflicto con cualquier otra.

Pero no te preocupes. Existe un metodo autenticamente ninja para **instalar paquetes desde el codigo fuente**, sin que enraicen en tu sistema sin control. Se llama ** stow** y no tardaras ni 10 minutos en enamorarte de él.

Instalarlo es tan facil como instalar cualquier fuente. Lo tipico es meterlo en _/usr/local/stow_. Una vez instalado, todos los fuentes que instales iran a parar a esta carpeta, y stow se encargara de enlazarlo simbolicamente en la ubicacion deseada.

1.  baja el stow

		wget http://ftp.gnu.org/gnu/stow/stow-latest.tar.gz


*  **OJO**: en algunas distros, falla por falta de una dependencia. Es necesario instalar un modulo de perl, test::output. 
*  Para instalar el modulo en **Debian** y similares:

		aptitude install  libtest-output-perl 

*  Para instalar en **RedHat**, **CentOS** y similares, puedes hacer:

		yum install perl-Test-Output


2.  Configura y makea como siempre

		./configure
	        make


3.  El unico detalle a tener en cuenta es el makeinstall, al cual tenemos que pasarle el prefijo de instalacion que queremos.

	     make install --prefix=/usr/local/ stow

4.  Un solo paso final, añadir la ruta al bin del stowa nuestro $PATH. Puedes hacerlo editando el fichero _~/.bash_profile_ para añadirlo al usuario actual, o a /etc/profile para añadirlo al sistema. O al archivo correspondiente en tu distribucion.

Y pista!!
Ya lo tenemos instalado. Ahora, cuando instales cualquier paquete, en el momento de hacer el configure, tienes que especificar el prefix de instalacion con una ruta dentro del stow, digamos

	     ./configure --prefix=/usr/local/ stow/paquete-1.2

Y continuar con las opciones habituales de _make && make install_.

Y en caso de que seas lo mas vago del mundo, tambien puedes usar este scripazo para instalarlo con la minga... Eso si, asegurate de cambiar antes las variables para ajustarlas a tu sistema, y tener las dependencias de perl (test::output) instaladas.
_Ejecutar como root_

	     #!/bin/bash
	     #### CONFIGURACION ####
	     # ruta donde quieres instalar el stow
	     ruta=/usr/local/stow     
	     # URL de descarga del  bluetooth
	     paquete=http://ftp.gnu.org/gnu/stow/stow-latest.tar.gz
	
	     #### BEGIN ####
	     cd /usr/src
	     wget $paquete
	     tar -xvvf stow*.tar.gz
	     cd $stowver
	     ./configure
	     make
	     make install --prefix=$ruta
	
	     echo "felicidades, ya tienes el stowinstalado"
	     echo "IMPORTANTE: acuerdate de añadir la ruta al ejecutable a tu $PATH"

Y con esto basta. A seguir trabajando, y no dejes de suscribirte al blog, para leer futuros articulos sobre **las herramientas mas utiles para evitar el stress del dia a dia de un sysadmin.**


