#  Práctica 1: Configuración de máquina virtual en el IaaS
[Página web](https://ull-esit-inf-dsi-2021.github.io/ull-esit-inf-dsi-20-21-prct01-iaas-Zarlie/)

## Introducción
En esta práctica llevaremos a cabo la configuración de la máquina virtual que encontraremos disponible a través del servicio IaaS de la ULL, además de la instalación y configuración de todas las herramientas necesarias para comenzar a trabajar en la asignatura de Desarrollo de Sistemas Informáticos.

## Objetivos
- Configurar la máquina virtual con la que trabajaremos en la asignatura
- Familiarizarnos con el uso de Github y más concretamente, profundizar en el uso de Github Pages
- Hacer uso de las herramientas Markdown y Jekyll

## Configuración de la máquina virtual en el IAAS
### **Configuación de la VPN y acceso al IaaS**  
En primer lugar, para comenzar esta práctica debemos configurar el servicio VPN de la ULL en caso de que nos encontremos fuera de la red universitaria, ya que sin ella no podremos acceder al servicio del IaaS. Para ello, debemos acceder a la [documentación de configuración de la VPN de la ULL](https://www.ull.es/servicios/stic/2020/12/01/servicio-de-vpn-de-la-ull/) y descargar las instrucciones correspondientes a nuestro sistema operativo: Windows, Linux, MAC OSX, Android, IOS. Una vez configurado el servicio de VPN, trataremos de conectarnos a la VPN de la ULL para proceder con la práctica.

Una vez estemos conectados a la VPN, accederemos al [Servicio IaaS de la ULL](https://iaas.ull.es/) donde introduciremos nuestras credenciales ULL. Acto seguido, se mostrará un panel en el que puede que nos encontremos con más de una máquina virtual, las cuales correspondan a otras asignaturas del grado asociadas a nuestra cuenta. Ahora nos tocará localizar la máquina virtual de la asignatura la cual tendrá el nombre de *DSI* y pulsaremos sobre el botón de *Ejecutar*. Tras esperar unos segundos, podremos visualizar que se nos ha asignado una máquina virtual del pool de máquinas virtuales de la asignatura, ya que nuestra máquina pasará a tener un número como sufijo, por ejemplo, en mi caso trabajaré con la máquina DSI-36.

### **Dirección IP de la máquina y conexión a la misma por SSH**      
Una vez dentro de nuestra máquina virtual, buscaremos en la parte derecha de la interfaz la sección de *Interfaces de red*, en ella podremos identificar la IP asignada a la interfaz de nuestra máquina la cual estará bajo la forma 10.6.XXX.XXX; en nuestro caso será 10.6.131.205. Esta IP nos servirá de ayuda para poder conectarnos por SSH a nuestra máquina virtual. 

Ahora bien, sabiendo que ya nos encontramos conectados a la VPN de la ULL para trabajar con la máquina virtual del IaaS y que poseemos la IP de dicha máquina, ya podremos conectarnos a ella por SSH. Para ello debemos abrir una terminal en nuestra máquina local y teclear lo siguiente:  
```
ssh usuario@10.6.XXX.XXX
```
Como podemos observar, hemos ejecutado el comando ssh acompañado de un nombre de usuario y una dirección IP; en este caso, el nombre de usuario será "usuario" y la IP, la dirección IP que obtuvimos en el paso previo. Ahora nos aparecerá el siguiente mensaje, donde tendremos que introducir **"yes"**:
```
The authenticity of host '10.6.131.205 (10.6.131.205)' can't be established.
ECDSA key fingerprint is SHA256:1Xm4M66FeBUSiykP7SqJgObwjmVs2gEouBhy1PTWDV4.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```
Ahora nos solicitará que introduzcamos una constraseña, la cual por defecto es "usuario". Una vez introducida, el sistema nos pedirá que la modifiquemos siguiendo 3 sencillos pasos: introducir la contraseña actual (usuario), introducir la nueva contraseña, y confirmar de nuevo la nueva contraseña. Una vez realizado este paso, tendremos que iniciar una nueva conexión SSH con nuestra máquina introduciendo esta vez la nueva contraseña.


### **Modificación del nombre de host de la máquina virtual**     
Una vez cambiada la contraseña, procederemos a modificar el nombre de host de la máquina virtual. Para ello, ejecutaremos en la terminal el comando cat accediendo al fichero /etc/hostname para conocer el nombre actual del sistema (nombre del equipo):
```
usuario@ubuntu:~$ cat /etc/hostname
ubuntu
```
Como podemos ver, actualmente el nombre del equipo es "ubuntu", este lo podremos cambiar ejecutando el comando vi o vim para abrir un editor de texto y establecer el nombre que queramos. En nuestro caso, lo identificaremos bajo el nombre de nuestra máquina virtual *iaas-dsi36*:
```
usuario@ubuntu:~$ sudo vim /etc/hostname
usuario@ubuntu:~$ cat /etc/hostname
iaas-dsi36
```
Además, también modificaremos el archivo /etc/hosts, donde se guarda la correspondencia entre dominios de Internet y direcciones IP:
```
usuario@ubuntu:~$ cat /etc/hosts
127.0.0.1   localhost
127.0.1.1   ubuntu

#The following lines are desireble for IPv6 capable hosts
::1       localhost ip6-localhost ip6-loopback
ff02::1   ip6-allnoders
ff02::2   ip6-allrouters
usuario@ubuntu:~$ sudo vim /etc/hosts
usuario@ubuntu:~$ cat /etc/hosts
127.0.0.1   localhost
127.0.1.1   iaas-dsi36
...
```




## Instalación de git y Node.js en la máquina virtual del IaaS
