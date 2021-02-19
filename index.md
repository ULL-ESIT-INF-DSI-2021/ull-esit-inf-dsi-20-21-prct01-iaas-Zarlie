#  Desarrollo de Sistemas Informáticos - Configuración de máquina virtual en el IaaS

## Introducción
En esta práctica llevaremos a cabo la configuración de la máquina virtual disponible a través del servicio IaaS de la ULL, además de la instalación y configuración de todas las herramientas necesarias para comenzar a trabajar en la asignatura de Desarrollo de Sistemas Informáticos.

## Objetivos

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text


## Configuración de la máquina virtual en el IAAS
En primer lugar debemos configurar el servicio VPN de la ULL en el caso de que estemos tratando de utilizar el servicio IaaS desde fuera de la red universitaria. Para ello, debemos acceder a la [documentación de configuración de la VPN de la ULL](https://www.ull.es/servicios/stic/2020/12/01/servicio-de-vpn-de-la-ull/) y descargar las instrucciones correspondientes a nuestro sistema operativo. Siga dichas instrucciones y trate de conectarse a la VPN de la ULL.

Una vez conectado a la VPN, deberá acceder al Servicio IaaS de la ULL e introducir sus credenciales ULL. A continuación, se le mostrará un panel de control con las diferentes máquinas virtuales que tiene asociadas a su cuenta. Si no lo ha hecho antes, deberá iniciar la máquina virtual que se llama DSI. Al arrancar dicha máquina, se le asignará una máquina virtual del pool de máquinas virtuales de la asignatura. Sabrá que lo anterior ha sucedido debido a que su máquina pasará a tener un número como sufijo, por ejemplo DSI-76.

Haga clic en el nombre de su máquina virtual y, en la parte derecha de la interfaz, donde se indica Interfaces de red, podrá conocer la IP asignada a la interfaz de su máquina. Conociendo dicha IP, ya podrá conectarse por SSH a su máquina. Es importante recordar que siempre tiene que estar conectado a la VPN de la ULL para trabajar con una máquina virtual del IaaS. Para conectarse por SSH a su máquina virtual, abra una terminal y teclee lo siguiente:

## Instalación de git y Node.js en la máquina virtual del IaaS
