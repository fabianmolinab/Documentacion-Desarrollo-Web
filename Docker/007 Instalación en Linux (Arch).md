# Instalación en Linux (Arch)


1. `sudo pacman -Syyu` ⇒ Actualizamos paquetes
2. `sudo pacman -S docker` ⇒ Instala docker
3.  `cd /var/run` ⇒ Dirigimos a run donde se aloja docker
4. `sudo chmod 777 -R docker.sock` ⇒ Modificamos los permisos del ejecutable docker
5. `docker info` ⇒ Verificamos si los permisos estan bien, para no tener que utilizar el super usuario al ejercutarlo
6. `sudo systemcl start docker.service`
7. `sudo usermod -aG docker $USER`
8. `docker run hello-word`