# Tipos Literales

Fechas: September 29, 2021 2:01 AM
Tipos: Clase

Cuando deseamos restringir un parámetro a una serie de valores posibles

```jsx
type LoginOperation = {
	op: 'login',
	username: string,
}

let l: LoginOperation = {
	username: 'fabian',
	op: 'login'
}
```

En el ejemplo el tipo **op** tiene que ser exactamente igual...

### Uniones entre los tipos

La primera forma de combinar tipos es utilizando uniones. En una unión los tipos que forman parte de esta se le llaman miembros.

```jsx
function convertir(valor: string | number){
	if (typeof(valor) === "string"){
		valor.trim()
 } else if (typeof(valor) === "number") {
	valor.toFixed()
}
}
```

Se utiliza `string | number` para definirlos como ambos, osea que el parámetro de la función puede ser un `string` o un `number`

Por medio de un condicional podemos trabajar con los tipos, diferentes asignando código o funcionalidad que requeramos, utilizando `typeof` para nos define el tipo de dato que está entrando. 

### Uniones discriminantes

```jsx
type OperacionSuma = {
	sumando1: number
	sumando2: number
	tipo: 'suma'
}
type OperacionMultiplicar = {
	operando1: number,
	operando2: number,
	tipo: 'multiplicar'
}

type Operacion = OperacionSuma | OperacionMultiplicar

function operar(o: Operacion) {
	if (o.tipo == 'suma') {

		return o.sumando1 + o.sumando2

	} else if (o.tipo == 'multiplicar') {

		return o.operando1 * o.operando2
	}
}

let resultado = operar({operando1: 1, operando2: 2, tipo: 'multiplicar'});
console.log(resultado);
```

En este ejemplo pasado combinamos las uniones con tipos estrictos para discriminar de unos de tipos de otros. El tipo 'suma' siempre sera de este tipo, en este caso podemos hace una relación entre los **`const`** y **`let`** Los primeros no se pueden cambiar una inicializados, por lo tanto una constante siempre va ser del mismo tipo, en el ejemplo de arriba vendría siendo cualquier de los **`tipos:`** ; en el caso contrario **`let`** si podría cambiar a lo largo de la operación vendría siendo cualquier de los operando que pueden ser cualquier **`number`**

### Intercepciones de tipos