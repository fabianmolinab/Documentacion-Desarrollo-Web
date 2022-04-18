# Agregar un repositorio remoto y SSH

Tags: SSH

## Agregar repositorio remoto

1. `git remote add origin [link clone]`
2. `git remote -v` ⇒ Muestra el repositorio remoto actual
3. `git pull origin master` ⇒ Trae los cambios del repositorio remoto
4. `**git push origin master` ⇒ Envía los cambios al repositorio remoto**

**Nota:** Si no deja pushear los cambios tipea el siguiente `git pull origin master —allow-unrelated-histories`

## Creando las llaves SSH en Git Hub

1. `git config -l`
2. `git config —-global user.mail`
3. Nos ubicamos en la carpeta de `usuario ~` 

**Creando las llaves**

1. `**ssh-keygen -t rsa -b 4096 -C "correo de git"**`
2. Digitamos las contraseñas
3. Buscamos la llaver en el directorio seleccionado
4. `eval $(ssh-agent -s)` ⇒ *Evaluamos que la llave este activa*
5. `ssh-add [directorio de la llave]` ⇒ *Agregamos la llave privada*
6. Copiamos el contenido del archivo ***rsa.pub***
7. Perfil de `Github/Setting/SSH and GPG Keys`
8. `New SSH key` ⇒ *Agregamos la llave publica*