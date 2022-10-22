# Comandos basicos

`docker run` ⇒ Corre un contenedor

`docker ps` ⇒ Muestra los contenedores activos

`docker ps -a` ⇒ Lista los contenedores historicos

`docker inspect [id del contenedor o alias]` ⇒ Muestra toda la información del contenedor

`docker run --name [alias] [nombre del contenedor]` ⇒ Corre un contenedor con un alias definido

`docker rename [nombre del contenedor] [nombre nuevo]` ⇒ Renombrar un contenedor

`docker rm [id o nombre]` ⇒ Borrar un contenedor

`docker container prune` ⇒ Borrar todos los contenedores inactivos

`docker run -it [nombre del contenedor]` ⇒ Corre en modo interactivo

**`docker stop [alias]` ⇒ (apaga el contenedor)

**`docker rm [alias]` ⇒ (borro el contenedor)

**`docker rm -f [alias]` ⇒ (lo para y lo borra)