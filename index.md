#  Desarrollo de Sistemas Informáticos - Configuración de máquina virtual en el IaaS
[Página web](https://ull-esit-inf-dsi-2021.github.io/ull-esit-inf-dsi-20-21-prct01-iaas-Zarlie/)

## Introducción
En esta práctica llevaremos a cabo la configuración de la máquina virtual disponible a través del servicio IaaS de la ULL, además de la instalación y configuración de todas las herramientas necesarias para comenzar a trabajar en la asignatura de Desarrollo de Sistemas Informáticos.

## Objetivos


## Configuración de la máquina virtual en el IAAS
En primer lugar debemos configurar el servicio VPN de la ULL en el caso de que estemos tratando de utilizar el servicio IaaS desde fuera de la red universitaria. Para ello, debemos acceder a la [documentación de configuración de la VPN de la ULL](https://www.ull.es/servicios/stic/2020/12/01/servicio-de-vpn-de-la-ull/) y descargar las instrucciones correspondientes a nuestro sistema operativo: Windows, Linux, MAC OSX, Android, IOS. Una vez configurado el servicio de VPN, trataremos de conectarnos a la VPN de la ULL para proceder con la práctica.

Una vez estemos conectados a la VPN, accederemos al [Servicio IaaS de la ULL](https://iaas.ull.es/) e introduciremos nuestras credenciales ULL. A continuación, se mostrará un panel de control con las diferentes máquinas virtuales que tenemos asociadas a nuestra cuenta. Si no se ha realizado con anterioridad, deberemos iniciar la máquina virtual bajo el nombre de DSI. Al arrancar dicha máquina, se le asignará una máquina virtual del pool de máquinas virtuales de la asignatura. Sabrá que lo anterior ha sucedido debido a que su máquina pasará a tener un número como sufijo, por ejemplo DSI-76.

Haga clic en el nombre de su máquina virtual y, en la parte derecha de la interfaz, donde se indica Interfaces de red, podrá conocer la IP asignada a la interfaz de su máquina. Conociendo dicha IP, ya podrá conectarse por SSH a su máquina. Es importante recordar que siempre tiene que estar conectado a la VPN de la ULL para trabajar con una máquina virtual del IaaS. Para conectarse por SSH a su máquina virtual, abra una terminal y teclee lo siguiente:

## Instalación de git y Node.js en la máquina virtual del IaaS
