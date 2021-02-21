#  Práctica 1: Configuración de máquina virtual en el IaaS
[Página web](https://ull-esit-inf-dsi-2021.github.io/ull-esit-inf-dsi-20-21-prct01-iaas-Zarlie/)

## Introducción
En esta práctica llevaremos a cabo la configuración de la máquina virtual que encontraremos disponible a través del servicio IaaS de la ULL, además de la instalación y configuración de todas las herramientas necesarias para comenzar a trabajar en la asignatura de Desarrollo de Sistemas Informáticos.

## Objetivos
- Configurar la máquina virtual con la que trabajaremos en la asignatura
- Familiarizarnos con el uso de Github y más concretamente, profundizar en el uso de Github Pages
- Hacer uso de las herramientas Markdown y Jekyll

## Configuración de la máquina virtual en el IAAS
### Configuación de la VPN y acceso al IaaS

En primer lugar, para comenzar esta práctica debemos configurar el servicio VPN de la ULL en caso de que nos encontremos fuera de la red universitaria, ya que sin ella no podremos acceder al servicio del IaaS. Para ello, debemos acceder a la [documentación de configuración de la VPN de la ULL](https://www.ull.es/servicios/stic/2020/12/01/servicio-de-vpn-de-la-ull/) y descargar las instrucciones correspondientes a nuestro sistema operativo: Windows, Linux, MAC OSX, Android, IOS. Una vez configurado el servicio de VPN, trataremos de conectarnos a la VPN de la ULL para proceder con la práctica.

Una vez estemos conectados a la VPN, accederemos al [Servicio IaaS de la ULL](https://iaas.ull.es/) donde introduciremos nuestras credenciales ULL. Acto seguido, se mostrará un panel en el que puede que nos encontremos con más de una máquina virtual, las cuales correspondan a otras asignaturas del grado asociadas a nuestra cuenta. Ahora nos tocará localizar la máquina virtual de la asignatura la cual tendrá el nombre de *DSI* y pulsaremos sobre el botón de *Ejecutar*. Tras esperar unos segundos, podremos visualizar que se nos ha asignado una máquina virtual del pool de máquinas virtuales de la asignatura, ya que nuestra máquina pasará a tener un número como sufijo, por ejemplo, en mi caso trabajaré con la máquina DSI-36.

### Dirección IP de la máquina y conexión a la misma por SSH    
Haga clic en el nombre de su máquina virtual y, en la parte derecha de la interfaz, donde se indica Interfaces de red, podrá conocer la IP asignada a la interfaz de su máquina. Conociendo dicha IP, ya podrá conectarse por SSH a su máquina. 

Es importante recordar que siempre tiene que estar conectado a la VPN de la ULL para trabajar con una máquina virtual del IaaS. Para conectarse por SSH a su máquina virtual, abra una terminal y teclee lo siguiente:


## Instalación de git y Node.js en la máquina virtual del IaaS
