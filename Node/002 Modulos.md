# Modulos

Funcionalidad organizada en uno o varios archivos de JavaScript que puede ser reutilizada en una aplicación. Por la complegidad de algunas aplicaciones Node nos permite importar modulos entre ellos, siendo mucho mas facil mantener las aplicaciones y paginas web, reutilizar codigo, corregir bugs y mucho más fácil de agregar nuevas funcionalidades. 

## Ejemplo

**Modulo a exportar**
```js
function saludar(nombre) {
	return `Hola ${nombre}`
}
module.exports.saludar = saludar
```

**Modulo a importar** 
```js
const saludo = require("./saludo.js")

console.log(saludo.saludar("freeCodeCamp"))
```

##  Importar varios modulos

```js
function saludar(nombre) {
	return `Hola ${nombre}`
}

function holamundo() {
	return 'Hola Mundo'
}

module.exports = {
	saludar: saludar,
	holamundo: holamundo
}
```
En este caso realizamos un objeto con las funciones o tipos de datos que vas a importar

### Desestructuración

```js
const { saludar } = require('./saludo.js')

console.log(saludar('hola'))
```

En el ejemplo anterior se puede usar desestructuración para la función **require** , desestructura los objetos dentro de la función teniendo solo los modulos desestructurados disponibles.

## Modulos built-in
Son modulos comunes para realizar tareas comunes al trabajar con Node.js, entre los mas comunes: 
- http
- https
- fs (file sistem)
- os (operative sistem)
- path

### Modulo consola `console`

Modulo incorporado en Node similar a la consola de un navegador, al colocar `console.log()` dentro de los metodos utiles de console tenemos: 
- console.log()
- console.warn()
- console.error()
- console.assert()
- **console.table()** 

#### Ejemplo
**console.error**
```js 
console.error(new Error('¡Hay un error!'))
// Mostrará un error en consola justo en la linea del codigo
```

**console.table:** Muestra una tabla con todos los argumentos y parametros util para objetos y strings.
```js
console.table(objeto)

// Muestra en forma de tabla todos los argumentos del objeto
```

### Modulo process

Procesa información sobre le proceso de node que se esté ejecutando. Dentro de sus metodos encontramos varios interesantes: 

- **argv:**  contiene información de la direcciones donde se ejecuta node, el programa, argumentos dentro del programa. 
    `console.log(process.argv)`
- **memoryUsange:** se usa para saber cuanta memoria se esta utilizando.
   `console.log(process.memoryUsange())`

### Modulo OS

Contiene funcionalidad para obtener información sobre el sistema operativo en el cual se ejecuta la aplicación. Entre los metodos tenemos: 

- **type:** devuelve información del sistema operativo donde se ejecuta node. `console.log(os.type())`
- **homedir:** devuelve el directorio raiz del sistema. `console.log(os.homedir())`
- **uptime:**  tiempo de ejecución del sistema en segundos. `console.log(os.uptime())`
- **userInfo:** Información del usuario. `console.log(os.userInfo())`

### Modulo timers

Contienes funciones que ejecutan codigo luego de cierto periodo de tiempo.

- **setTimeout():** Para ejecutar codigo luego de un número específico de milisegundos.  Sintaxis `setTimeout(funcion, retraso, argumento)`.
	  ***Ejemplo:*** 
	```js
		function mostrarTema(tema) {
			console.log(`estoy aprendiendo ${tema}`)
		}
		setTimeout(mostrarTema, 1000, 'node.js')
  ```
  
 - **setImmediate():** Para ejecutar codifo asincrono en la proxima iteración del ciclo de eventos, ejecutara despues del codigo sincrono. ***Sintaxis*** => `setImmediate(funcion, argumento1, argumento2)`
 
	***Ejemplo:*** 
	```js
	function mostrarTema(tema) {
			console.log(`estoy aprendiendo ${tema}`)
	}
	console.log('Antes')

	setImmediate(mostrarTema, 'node.js')
	console.log('Despues')
	//Respuesta:
	//Antes 
	//Despues
	//estoy aprendiendo node.js
  ```
  
 - **setInterval():** Para ejecutar un numero infinito de veces con un retraso especifico de milisegundos. ***Sintaxis =>*** `setInterval(funcion, intervalo,argu1, argu2)`   

### Modulo fs 

Contiene funcionalidad muy util para trabajar con el sistema de archivos. Entre sus operaciones con archivos podermos: leer, modificar, copiar, eliminar y cambiar nombre. 
Todos los métodos de este módulo son asincronos por defecto, tambien puedes escoger versiones sincronas de los metodos agregando **Sync** a sus nombres. 

#### readFile

Se usa para leer el contenido de un archivo. Agregando Sync despues del nombre del metodo podemos tener la operación sincrona.  *fs.readFileSync*

**Ejemplo:**
```js 
const fs = require('fs')

fs.readFile('index.html','utf-8', (err, contenido) => {
  if (err) {
	console.log(err)
  } else {
    console.log(contenido)
  }
})
```

#### rename

Cambia el nombre de un archivo

**Ejemplo:**
```js
const fs = require('fs')

fs.rename('nombreDelArchivo', 'NuevoNombre', (err) => {
  if(err) {
    throw err
  }
  console.log('Cambiado')
})
//Cambia el nombre
```

#### appendFile

Agregar contenido al final de un archivo.

**Ejemplo:**
```js 
const fs = require('fs')

fs.appendFile('nombreDelArchivo', '<contenido>', (err) => {
  if(err) {
    throw err
  }
  console.log('agregado el contenido')
})
```


#### writeFile

Reemplazar todo el contenido de un archivo.

```js
const fs = require('fs')

fs.writeFile('nombreDelArchivo', 'Contenido Nuevo', (err) => {
  if(err) {
	throw err
  }
  console.log('Contenido Reemplazado')
})
```

#### unlink

Eliminar Archivo

**Ejemplo:** 
```js
const fs = require('fs')

fs.unlink('nombreDelArchivo', (err) => {
  if(err) {
    throw err
  }
  console.log('Archivo Borrado')
})
```