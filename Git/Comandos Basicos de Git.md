# Comandos basicos

Descripción: Algunos comandos basicos y los estados de Git
Tags: Basico

## ¿Como inciar un repositorio?

`**git init**`

Se creará una carpeta .**git** oculta en el directorio de la carpeta iniciada

## Configuración de usuario

- `**git config --global user.email` **usuariodeMail**
- `**git config --global user.name**`  **usuriodeGitHub**

## Estados de Git

1. **Working Directory:** 
    
    Este es el estado inicial de los archivos al ingresar `**git init**`  
    
2. **Staging Area:**
    
    Para entrar a este estado `git add` nombre del archivo o `.` ⇒ para todos los archivos 
    
3. **Repositorio Local:**
    
    Tipeamos `git commit -m ""` para pasar los archivos de Staging Area a el Repositorio Local, esto se hace cuando tenemos todos los cambios hechos.  
    
    ***Nota:*** *"" Se hace una pequeña descripción del commit*
    

## Mandar y traer archivos al Repositorio Remoto en GitHub

`**git push` **⇒ Mandar archvos al repositorio remoto**

`**git pull**` **⇒ Trae archivos del repositorio remoto al local**

## Eliminar Archivos

`**git rm**` ⇒ Remover Archivos

`**git rm --cached**` ⇒ Remover los archivos del cache o staging area

## Otros comandos

`**git clone` ⇒** Clona los repositorios 

`**git show` ⇒** Muestra el historial de cambios

`**git push` ⇒** Compara commits

## ¿Que es el HEAD?

Head es el ultimo commit en la rama donde estamos.
