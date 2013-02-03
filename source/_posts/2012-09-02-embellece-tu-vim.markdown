---
layout: post
title: "embellece tu vim - instalar un gestor de plugins y un tema en 5 minutos"
date: 2012-09-02 21:04
comments: true
categories: userland, miniarticle
---

_Tiempo de lectura estimado: **2 minutos 34 segundos**_


Si estas empezando con vim, y todavia te da un poco de respeto utilizar plugins, temas, y esa clase de cosas, o no tienes tiempo para "ponerte a mirarlo", este post es para ti.

Una aproximacion a uno de los varios sistemas de **gestion de plugins para vim**, acompañada de la instalacion de un primer plugin para la gestion de codigo con Git (_Fugitive_) y un tema (_Solarized_)

Antes de ponerte con este tutorial, deberias tener _git_ instalado, aunque no es imprescindible.


## Gestion de plugins en vim

[Pathogen](https://github.com/tpope/vim-pathogen) es un sistema de gestion de plugins para el editor de texto _Vim_. Gracias a el podemos instalar nuestros plugins de vim en directorios separados, de forma ordenada, y ademas, alejada del .vimrc (y no voy a evangelizar ahora sobre las ventajas de la [modularizacion](http://es.wikipedia.org/wiki/Modularidad_(inform%C3%A1tica)) ;) 

## La miga, instalando Pathogen

Primero **creamos los directorios** que usaremos para instalar los plugins


		$ cd ~
		$ cd .vim
		$ mkdir  autoload
		$ mkdir bundle


Nos movemos al directorio desde donde pathogen carga los plugins, y **lo descargamos**


		$ cd autoload/  
		$ curl -so pathogen.vim  https://raw.github.com/tpope/vim-pathogen/master/autoload/pathogen.vim


Si no tienes curl, siempre puedes usar "" wget -0 pathogen.vim https.... ""
Si estas utilizando windows, en lugar de trabajar sobre ""~/.vim"", deberias hacerlo sobre ""~/vimfiles"" 

**Editamos nuestro _.vimrc_**. Si eres nuevo en vim, tendras que crear uno nuevo. Copia y pega este modelo basico que incluye la llamada a pathogen:


		call pathogen#infect()
		syntax on
		filetype plugin indent on


A partir de ahora, todos los plugins que descomprimas dentro de ""~/.vim/bundle"" seran automaticamente añadidos a tu "runtimepath". 


## Instalando un plugin

Vamos a comprobarlo **instalando [Fugitive](http://vimcasts.org/episodes/fugitive-vim---a-complement-to-command-line-git/) **:


		$ cd ~/.vim/bundle
		$ git clone git://github.com/tpope/vim-fugitive.git

Y ya esta instalado! :) 
Si no tienes git instalado, puedes descargarlo igualmente, descomprimirlo, y moverlo al directorio bundle.



## Instalacion de un esquema de colores

Instalar temas de colores es similar a la instalacion de plugins. Vamos a instalar un esquema bastante bien cuidado, con 2 modos, claro y oscuro. [Solarized](https://github.com/altercation/vim-colors-solarized)

		$ cd ~/.vim/bundle
		$ git clone git://github.com/altercation/vim-colors-solarized.git


Si todavia no usas _Git_, siempre puedes descargarlo, y moverlo al directorio:


		$ mv vim-colors-solarized ~/.vim/bundle/


Y ahora modificamos nuestro .vimrc para adoptar nuestro nuevo esquema. Añade este texto


		set backgroud=dark
		colorscheme solarized


Si prefieres algo mas clarito, basta con cambiar "dark" por "light".

En caso de que quieras usar este tema de vim en el terminal (no en la version grafica de vim o un emulador de terminal) es recomendable que configures tambien tu terminal para utilizar el esquema de solarized. Sino, no estaras viendo los autenticos colores, sino una degradacion a la paleta ansi estandar de 256 colores.


Espero que sea util, y a partir de ahora mejores tu uso de vim con los numerosos plugins que existen.


## Referencias y mas lectura relaccionada

*  [Documentacion oficial de pathogen](https://github.com/tpope/vim-pathogen)
*  [Screencast sobre Fugitive](http://vimcasts.org/episodes/fugitive-vim---a-complement-to-command-line-git/)
*  [Documentacion sobre Solarized para vim](http://ethanschoonover.com/solarized/vim-colors-solarized)
*  [Repositorio de Solarized para Vim](https://github.com/altercation/vim-colors-solarized)

