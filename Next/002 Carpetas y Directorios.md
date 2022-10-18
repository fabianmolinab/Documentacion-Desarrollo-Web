# Carpetas y directorios


### .next/

Es la parte oculta que lanza el servidor next por defecto, muchas de las características de la aplicación que se lanza a producción está en esta carpeta, se puede borrar y se crea nuevamente al lanzar el servidor de desarrollo.

### pages/

Una de las funciones de Next es el rooter, que se comporta por medio de archivos y carpetas, dentro de la carpeta `pages/` se crean todas las rutas de la aplicación. Para este caso añadimos:

1. Una carpeta con el nombre de la ruta ejemplo *timeline* `pages/timeline` 
2. Dentro de esa carpeta añadimos un archivo `index.js`

Cada uno de los archivos dentro de esta carpeta se deben importar por defecto y los nombres deben empezar por minúscula.

#### pages/_app.js

Es un archivo en js o ts donde se inicia la aplicación. Desde este archivo se reenderiza todas las paginas o archivos que estén dentro de la carpeta *pages*

### public/

Esta carpeta se usa para mandar archivos estáticos que no van a ser compilados, generalmente se usa para imágenes, iconos, textos.



