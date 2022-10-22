# Objetos


```jsx
//Primera forma
let usuario: {
	nombre: string;
	apellidos: string;
	edad: number;
	pais: string;
	casado: boolean;
	pareja: {
		nombre: string;
		apellido: string;
		edad: number;
	};
} = {
	nombre: 'fabian',
	apellidos: 'molina',
	pais: 'Colombia',
	edad: 26,
	casado: false,
	pareja: {
		nombre: 'Dayana',
		apellido: 'Salcedo',
		edad: 26,
	},
};
//Segunda forma
let objeto: object = {
	nombre: 'Juliana',
	edad: 12
}
```

Los objetos se pueden realizar de una u otra forma, la primera para el tipado estricto y la segunda es para el tipado dinamico, esta es mucho mejor utilizarla que  **any** ya que puede ser de cualquier tipo.