# Descartar cambios de archivos con Git

Enlaces: https://desarrolloweb.com/articulos/descartar-cambios-archivos-git.html
Tags: Basico

`git checkout -- [ruta del archivo]` ⇒ **Elimina cambios que no este ni en stating ni commiteados**

Esta linea regresa al últimos commit del archivo seleccionado

## Descartar todos los cambios en archivos modificados

Ahora imagina que has hecho cambios sobre varios archivos, pero no te gustaron y quieres volver al estado del último commit, eliminando de manera permanente todos los cambios a todos los archivos realizados.

Esta operación la consigues con el comando "git reset". La podrás realizar de la siguiente manera:

`git reset --hard`

La opción "--hard" provoca que cualquier cambio de archivos cuyo seguimiento llevamos con Git se elimine, volviendo al estado justo después del último commit. Eso quiere decir que, si hubiera archivos que no se han agregado todavía al repositorio (archivos nuevos desde el último commit), permanecerán en el espacio de trabajo.

## Descartar los cambios de un archivo que está en staging area

Pudiera darse el caso que hayas hecho "git add" de un archivo que ahora pretendes descartar. En ese caso ese archivo está almacenado provisionalmente, en el espacio que se conoce como "staging area".

La operativa anterior de reset funcionará también en este caso.

`git reset --hard`

Si haces "git reset --hard" esos cambios también se eliminarán, pero podría ocurrir que hayas hecho el add de varios archivos al staging area y sólo quieras resetear los cambios de uno de ellos. Entonces tendrías que usar el comando reset con una opción diferente (recuerda que "git reset --hard" descarta los cambios de todos los archivos). Para eliminar entonces estos cambios de un archivo único, primero tendríamos que sacar el archivo en concreto del staging area y luego descartar los cambios, con la combinación de estos dos comandos.

```
git reset HEAD archivo.txt
git checkout -- archivo.txt
```

## Descartar los cambios, pero guardar provisionalmente los archivos modificados

Hay una alternativa todavía un poco más compleja con el comando "git stash" para descartar cambios de un archivo, pero sin perderlos del todo, pudiendo volver al estado anterior de esos archivos más adelante. Esto puede ser útil en muchos casos, como por ejemplo cuando tienes que cambiar de rama pero no quieres hacer commit de los cambios porque tu trabajo te lo has dejado a medias. En ese caso podrías descartar los cambios, pero guardarlos para que, más adelante, puedas volver a ellos y seguir por donde lo habías dejado.

El comando "stash" es suficientemente complejo para verlo en un artículo independiente, pero veamos una operativa muy sencilla para que podamos solucionar este caso particular.

```
git stash
```

Entonces nos aparecerá un mensaje como este "Saved working directory and index state WIP on nombre_rama". WIP son las siglas de "work in progress".

Ahora verás que los archivos modificados están otra vez como en el estado del último commit. Podrías cambiar de rama o hacer cualquier cosa y, cuando quieras volver al estado de tus archivos almacenado como "work in progress", lanzarás el siguiente comando:

```
git stash pop
```

Eso provocará que los cambios guardados en stash vuelvan a colocarse en tu espacio de trabajo.

Si quieres ver el status de tu proyecto, con información sobre archivos que tengas en "Work In Progress" con stash, puedes hacer un comando como este:

```
git status --show-stash
```

## Conclusión

Con lo que hemos visto en este artículo tienes un completo set de alternativas cuando quieres descartar cambios en uno o varios archivos de un repositorio y volver al estado anterior del espacio de trabajo, justo después del último commit.

Te servirán de bastante ayuda en multitud de casos. Sólo cerciórate de estar seguro que quieres descartar los cambios, puesto que la operación es permanente (ya que no se había realizado ninguna confirmación de esos archivos modificados). Recuerda que si quieres, por cualquier motivo, dejarte abierta la posibilidad de recuperar esos cambios descartados, tendrás que usar la operativa de stash. Consulta nuestro [Tutorial de Git](https://desarrolloweb.com/manuales/manual-de-git.html) para seguir aprendiendo otras facetas del sistema de control de versiones.