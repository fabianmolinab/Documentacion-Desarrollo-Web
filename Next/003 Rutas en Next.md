# Rutas en Next

Una de las funciones de Next es el rooter, que se comporta por medio de archivos y carpetas, dentro de la carpeta `pages/` se crean todas las rutas de la aplicación. Para este caso añadimos:

1. Una carpeta con el nombre de la ruta ejemplo *timeline* `pages/timeline` 
2. Dentro de esa carpeta añadimos un archivo `index.js`

## Sistemas de Rutas SPA

Cuando queremos crear una ruta pero que no se recargue la paguina cada vez es decir un sistema (SPA) tenemos que indicarselo ya que por defecto con el router no está activado. Seria de la siguiente manera:

```jsx
import Link form 'next/link'

export const Home = () => {
	<Link href="/timeline"> Time Line</Link>
}

```

De esta forma será un link sin que se cargue nuevamente la pagina.


## Use Router
