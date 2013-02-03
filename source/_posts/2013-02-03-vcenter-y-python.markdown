---
layout: post
title: "How to list virtual machines from VCenter with Python"
date: 2013-02-03 01:55
comments: true
categories: programming, python, vmware, virtualization, automation
---

Me gusta automatizarlo todo, y muchas de las tareas que habitualmente realizo, estan relacionadas con VMWare, y principalmente con VCenter, VSphere, y servidores ESX o ESXi.
Llegado el dia, a ti te ha tocado tambien, asi que echale un vistazo a este post, y averigua como hacer tu propio informe de capacidad o de estado de tus servidores, con un
sencillo script en python.

## Como conectarse al vCenter
Hay unas cuantas maneras. puedes usar libvirt, que es mucho mas potente, o puedes usar pysphere. Ahora vamos a utilizar psphere. 
Podemos instalarlo con el tipico 

	pip install psphere

O con el gestor de paquetes de nuestra distribucion. (lo siento por los de windows... si alguien puede aportar la instalacion en windows, la enlazo encantado)o

Una vez instalado, primero tenemos que conectarnos con un "cliente", con el que luego haremos consultas e interactuaremos con el vCenter.


	from psphere.client import Client
	my_client = Client( server = "vc.domain.com", username = "Administrator", password = "secret")

## Como sacar datos sobre las maquinas

Primero tendremos que sacar un listado de todas las maquinas. Podemos hacerlo con dos aproximaciones. Sacando directamente todas las maquinas del vcenter a partir de un objeto de maquina virtual:

	from psphere.managedobjects import VirtualMachine
	vms = VirtualMachine.all(my_client)
	for vm in vms:
	    print vm.name

O dividiendolo por host:

	from psphere.managedobjects import HostSystem  
	for host in HostsSystem.all(my_client):
	    print "Hostname: ", host.name
	    vms = host.vm
	    for vm in vms:
	        print vm.name


## Avanzando mas alla

Y a partir de aqui, se abre un mundo de posibilidades. Yo por ejemplo, creo periodicamente informes de estado de mi entorno de virtualizacion, y lo subo a la wiki de mi empresa, para que lo pueda ver todo el equipo de infraestructura.

