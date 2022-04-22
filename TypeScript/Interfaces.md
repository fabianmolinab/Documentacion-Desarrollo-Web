# Interfaces

Fechas: October 5, 2021 2:20 AM
Tipos: Clase

### Ejemplo común

```jsx
interface UserData {
	username: string;
	created_at: Date;
	superuser?: boolean;
}

function login(): UserData {
	return {
		username: "admin",
		created_at: new Date(),
		superuser: true,
	};
}
let data = login();
```

Este capitulo es uno de los importantes en el tipado, las interfaces las defino como esos requerimientos que hacemos para implementarlos luego, son como los planos de una casa se deben seguir al pie de la letra a la hora de construir la casa. En ejemplo anterior tenemos `interface` **UserData** que son los requerimientos en forma de objeto, que luego la función login le asignamos **UserData** como el valor que retorna la función. 

Login estrictamente debe tener los tipos de datos definidos en **UserData** que es la `interface` creada anteriormente, en caso que de omita o añada otro dato diferente este tendrá un error. He aquí la potencia de las interface. 

### Propiedades Opcionales y solo lectura

No todas las propiedades de una interface tienen que ser requeridas. Lo veremos con el siguiente ejemplo:

```jsx
interface UserData {
	username: string;
	created_at: Date;
	readonly superuser?: boolean;
}

function login(): UserData {
	return {
		username: "admin",
		created_at: new Date(),
		//superuser: true,
	};
}
let data = login();
```

Para definir propiedades dentro de las interfaces que no son requeridas lo hacemos con `?`  en este caso **superuser** no tiene que estar implementada. Cuando una propiedad dentro de la interfaz es de solo lectura solo se podra definir una vez en el objeto, no se podra modificar fuera del mismo. 

### Interfaces usándolas con clases

## Referencias y Articulos
* [[Uso de interfaces en TypeScript]] Enlace externo :D
* [[Parte 3 Interfaces [articulo]]] Uso de Interfaces