# Funciones

Fechas: September 13, 2021 12:33 AM
Tipos: Clase

```jsx
let boton1: {
	largo: number;
	ancho: number;
} = {
	largo: 20,
	ancho: 30,
};

export function boton( largo :number, ancho :number): number {
	let area = largo * ancho;

	console.log(
		`Las dimesiones de nuestro boton son ${largo}, ${ancho} y el area es ${area}`,
	);

	return area;
}

boton(boton1);
```

### Segunda forma

```jsx
let suma : (number1: number, number2: number ) => number = (number1, number2) => {

  let suma = number1 + numbser2;

  console.log(`El resultado de la suma es ${suma}`)
  return suma;
}
```