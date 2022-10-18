# Blocking y Non Blocking I/O

Una ejecución bloqueante no es mas que un codigo sincrono, es decir, al hacer peticiones o bucle while tiene tiempo de demora en ejecución se esperar que este termine para continuar. Por el contrario el no blocking o asicrono, no espera que la peticiones o el bucle termine para que se siga ejecutando sino que este sigue las siguientes instrucciones, esto permite una mejora en los tiempos de espera haciendo node lo suficientemente rapido.

## Ejemplos
**Blocking**
```js
const fs = require('fs'); 
const data = fs.readFileSync('/file.md'); 
console.log(data); 
moreWork(); // Se ejecuta despues del console.log
```
**No Blocking**
```js
const fs = require('fs'); 
fs.readFile('/file.md', (err, data) => { 
	if (err) throw err; 
	console.log(data); 
}); 
moreWork(); // Se ejecuta antes del console.log
```