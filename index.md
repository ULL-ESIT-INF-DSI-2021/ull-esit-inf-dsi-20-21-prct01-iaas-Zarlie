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


### **Modificación de los ficheros /etc/hostname y /etc/hosts**     
Una vez cambiada la contraseña, procederemos a modificar el nombre de host de la máquina virtual. Para ello, ejecutaremos en la terminal el comando cat accediendo al fichero /etc/hostname para conocer el nombre actual del sistema (nombre del equipo):
```
usuario@ubuntu:~$ cat /etc/hostname
ubuntu
```
Como podemos ver, actualmente el nombre del equipo es "ubuntu", este lo podremos cambiar mediante un editor de texto como vi o vim y establecer el nombre que queramos. En nuestro caso, lo identificaremos bajo el nombre de nuestra máquina virtual *iaas-dsi36*:
```
usuario@ubuntu:~$ sudo vim /etc/hostname
usuario@ubuntu:~$ cat /etc/hostname
iaas-dsi36
```
Además, también modificaremos el archivo /etc/hosts, donde se guarda la correspondencia entre dominios de Internet y direcciones IP. En él, cambiaremos el antiguo nombre de host ubuntu por el nombre de host (en mi caso iaas-dsi36):
```
usuario@ubuntu:~$ cat /etc/hosts
127.0.0.1   localhost
127.0.1.1   ubuntu

#The following lines are desireble for IPv6 capable hosts
::1         localhost ip6-localhost ip6-loopback
ff02::1     ip6-allnoders
ff02::2     ip6-allrouters

usuario@ubuntu:~$ sudo vim /etc/hosts
usuario@ubuntu:~$ cat /etc/hosts
127.0.0.1   localhost
127.0.1.1   iaas-dsi36
...
```
Una vez hayamos completado todos los pasos anterioremos, pasaremos a actualizar el software de la máquina virtual antes de proceder a reiniciarla. Para ello usaremos 2 comandos: **sudo apt update** el cual actualizará la lista de paquetes disponibles y sus versiones, sin instalar o actualizar ningún paquete en concreto, y el **sudo apt upgrade**, el cual una vez el comando anterior ha descargado la lista de software disponible y la versión en la que se encuentra, actualizará e instalará las nuevas versiones de los paquetes.
```
usuario@ubuntu:~$ sudo apt update
Leyendo lista de paquetes... Hecho
Creando árbol de independencias
Leyendo la información de estado... Hecho
...

usuario@ubuntu:~$ sudo apt upgrade
...
```
Finalmente, reiniciamos la máquina:
```
usuario@ubuntu:~$ reboot
Connection to 10.6.131.205 closed by remote host.
Connection to 10.6.131.205 closed.
```

## Configuraciones en la máquina local
Una vez acabado el reinicio, volveremos a editar el fichero de hosts, pero esta vez de la máquina local. En ella, añadiremos la información de conexión a la máquina virtual para no tener que estar recurriendo constantemente a la dirección IP de la máquina virtual:
```
zarlie@melinux-VirtualBox:~$ cat /etc/hosts
127.0.0.1     localhost
127.0.1.1     melinux-VirtualBox
...
zarlie@melinux-VirtualBox:~$ vim /etc/hosts
zarlie@melinux-VirtualBox:~$ cat /etc/hosts
127.0.0.1     localhost
127.0.1.1     melinux-VirtualBox
10.6.131.205  iaas-dsi36
...
```
El siguente paso será configurar la infraestructura de clave pública-privada en caso de no haberse hecho anteriormente:
```
zarlie@melinux-VirtualBox:~$  cat .ssh/id_rsa.pub
cat: .ssh/id_rsa.pub: No existe el archivo o el directorio
```
Como podemos observar, en este caso aún no se habían generado el par de claves pública-privada, ya que no parece existir ninún archivo que las contenga (id_rsa para la clave privada e id_rsa.pub para la clave pública). Ejecutaremos el comando **ssh-keygen** para crear el par de claves RSA el cual nos irá generando un script de generación de claves al cual simplemente nos limitaremos a dejar los valores por defecto, para ello dejaremos vacíos todos los campos en los que nos pidan introducir un valor. Es muy importante no introducir ninguna passphrase asociada al par de claves.
```
zarlie@melinux-VirtualBox:~$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/zarlie/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase:
Your identification has been saved in /home/zarlie/.ssh/id_rsa
Your public key  has been saved in /home/zarlie/.ssh/id_rsa.pub
...
```
Una vez generadas las claves, ejecutaremos el comando **ssh-copy-id**, este es un script que se conecta a la máquina y copia el archivo (indicado por la opción -i) en ~/.ssh/authorized_keys, y ajusta los permisos de forma adecuada. Nuevamente nos saldrá un mensaje de alerta de si queremos seguir con la conexión, al que deberemos introducir **"yes"** y acto seguido introduciremos nuestra contraseña y ya habremos añadido la clave:
```
zarlie@melinux-VirtualBox:~$ ssh-copy-id usuario@iaas-dsi36
The authenticity of host 'iaas-dsi36 (10.6.131.205)' can't be established.
ECDSA key fingerprint is SHA256:1Xm4M66FeBUSiykP7SqJgObwjmVs2gEouBhy1PTWDV4.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
usuario@iaas-dsi36's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'usuario@iaas-dsi36'"
and check to make sure that only the key(s) you wanted were added.
```
Como nos indica el último mensaje del comando anteriormente ejecutado, intentaremos iniciar sesión en la máquina virtual ejecutando el siguiente comando:
```
zarlie@melinux-VirtualBox:~$  ssh usuario@iaas-dsi36
Welcome to Ubuntu 18.04.5 LTS (GNU/Linux 4.15.0-135-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sun Feb  21 19:26:27 WET 2021

...

Last login: Sun Feb  21 19:26:27 2021 from 10.20.52.107
usuario@iaas-dsi36:~$
```
Como podemos observar, no ha habido ningún problema para acceder a la máquina virtual sin necesidad de tener que introducir una contraseña en la terminal. Por otro lado, el prompt de la máqina virtual también ha cambiado al nuevo nombre de host configurado previamente (en mi caso aparece como *usuario@iaas-dsi36~$*).  

La última configuación que nos queda hacer en la máquina local es la de configuar el fichero **~/.ssh/config** para conectarnos mediante SSH a nuestra máquina virtual sin la necesidad de indicar un nombre de usuario, simplemente indicando el nombre de nuestra máquina:
```
zarlie@melinux-VirtualBox:~$ touch ~/.ssh/config 
zarlie@melinux-VirtualBox:~$ vi ~/.ssh/config 
zarlie@melinux-VirtualBox:~$ cat ~/.ssh/config 
Host iaas-dsi36
  HostName iaas-dsi36
  User usuario
```

Ahora si tratamos de iniciar sesión simplemente indicando el nombre de nuestra máquina virtual podremos hacerlo:
```
zarlie@melinux-VirtualBox:~$ ssh iaas-dsi36
Welcome to Ubuntu 18.04.5 LTS (GNU/Linux 4.15.0-135-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sun Feb  21 19:38:00 WET 2021

...

Last login: Sun Feb  21 19:38:00 2021 from 10.20.52.107
usuario@iaas-dsi36:~$
```

## Configuraciones en la máquina local
Por último, nos queda generar las claves pública-privada en nuestra máquina virtual exactamente como hicimos anteriormente en nuestra máquina local:
```
usuario@iaas-dsi36:~$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/zarlie/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase:
Your identification has been saved in /home/zarlie/.ssh/id_rsa
Your public key  has been saved in /home/zarlie/.ssh/id_rsa.pub
...

usuario@iaas-dsi36:~$ cat .ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDfCKDPGn7qLhwmjKCYaCBeOZVObmdHQ/GFOYALTU1Lmnjb108HGSr7aDaFZunI1TtwAKh1qGdo6LYCPECY+y90LA+vtRTdQnoPqGzsTctillZkRJoMv7beLhpHVKFadXNc/DKlwCU83uHwTRGmqb3OY5246rSIA+/blFpDEBpK088oXvTailphaCeZRHV+Qg12LJu5Q2uKBTjckU0yebz4Xx2wXjZQkpohX8PSOJpKy6QlNmG8j3DDY+qrRmy+LScRGyWHlqQIVR2YrejuHqs2mG1b8FSGNwUUCp20rc0TWV22ggjQxEmjCRAHIofRsZ7zN752aChLqWGXcDJLTI8d usuario@iaas-dsi36
```



## Instalación de git y Node.js en la máquina virtual del IaaS
Comenzaremos instalando git en nuestra máquina virtual:
```
usuario@iaas-dsi36:~$ sudo apt install git
Leyendo lista de paquetes... Hecho
Creando árbol de dependencias       
Leyendo la información de estado... Hecho
git ya está en su versión más reciente (1:2.25.1-1ubuntu3).
Los paquetes indicados a continuación se instalaron de forma automática y ya no son necesarios.
...
```





## Bibliografía
- (https://debian-handbook.info/browse/es-ES/stable/sect.hostname-name-service.html)
- (https://www.ionos.es/digitalguide/servidores/configuracion/archivo-hosts/)
- (https://www.ionos.es/digitalguide/hosting/cuestiones-tecnicas/hostname/)
- (https://es.wikipedia.org/wiki/Archivo_hosts)
- (https://www.linuxhispano.net/2013/05/03/diferencia-entre-apt-get-update-y-apt-get-upgrade/)
- (https://www.tiendalinux.com/docs/manuales/redhat/rhl-rg-es-7.3/s1-ssh-configfiles.php3#:~:text=known_hosts%20%E2%80%94%20Este%20fichero%20contiene%20las,conectado%20al%20servidor%20SSH%20correcto.)
- (https://uniwebsidad.com/libros/pro-git/capitulo-4/generando-tu-clave-publica-ssh)
