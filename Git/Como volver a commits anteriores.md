# Como volver a commits anteriores
Sección para volver en el tiempo en #git  

1. **Ver los cambios específicos del archivo
`git log --stat`**

2. **Verificamos la versión anterior** 
**`git checkout [commit] [archivo]`**

3. **Volvemos a la versión actual** 
`git checkout master**`

4. **Para resetear al commit anterior**
* Cambios drásticos (poco recomendado )  **`git reset [commit] --hard`**
* Guarda cambios en staging   **`git reset [commit] --soft`**

## Volver a commit borrados por *`Reset Hard`*
1. `git reflog` ⇒ Para ver un historial de todo lo realizado en el repositorio
2. Copiamos el commit donde queremos ir
3. `git reset [commit] --hard` 


## Modificar mensajes de los commit

1. `git commit --amend -m "Mensaje"` ⇒ Modifica el mensaje del ultimo commit**

## Modificar un commit ya hecho

1. Verificamos el commit que queremos cambiar con `git log`
2. `git reset --soft HEAD^` Para retroceder el commit anterios a statting**
3. `git commit -m "mensaje"`  Realizamos el commit con los nuevos cambios

## Si nos da errores Resetear un Commit

`**git reset--hard <commit-id>**` ⇒ ubicar el ID del commit al cual queremos regresar

`**git reset--soft HEAD@{1}**` ⇒ indicar que este commit será el nuevo

`**git commit -m "Se revirtieron los cambios"**` ⇒ subir los cambios


### Referencias
**[[Descartar cambios de archivos en Git]]**
**[[Agregar commit de archivos individuales]]**
