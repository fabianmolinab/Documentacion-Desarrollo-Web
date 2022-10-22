# Clases

Fechas: September 13, 2021 1:09 PM
Tipos: Clase

## Ejemplo

```jsx
class Rectangulo {
	ancho: number;
	alto: number;

	constructor(ancho: number, alto: number) {
		this.ancho = ancho;
		this.alto = alto;
	}

	area() {
		return this.ancho * this.alto;
	}
	perimetro() {
		return this.ancho * 2 + this.alto * 2;
	}
}

let r1 = new Rectangulo(5, 3);
r1.area();
r1.perimetro();
```

### Visibilidad

Característica de TypeScript para restingir el acceso a cierto atributos y propiedades. Se le asigna simplemente colocando **private** antes del atributo o propiedad.

```ts
private ancho: number;
private alto: number;
```

### Readonly

Se utiliza para inmutar atributos es decir para que no puedan modificarse una vez inicializados. 

```ts
readonly ancho: number
readonly alto: number
```

### Ejemplo General

```ts
class Rectangulo {
	// Para evitar que leas y escribas dentro de la clase
	private readonly ancho: number;
	private readonly alto: number;

	constructor(ancho: number, alto: number) {
		this.ancho = ancho;
		this.alto = alto;
	}

	area() {
		return this.ancho * this.alto;
	}
	perimetro() {
		return this.ancho * 2 + this.alto * 2;
	}
}

let r1 = new Rectangulo(5, 3);
//r1.ancho = 6;
console.log(r1.area());
```

### Getters y Setters

te permite acceder y asignar sus propiedades

```jsx
export class Hero {
   private _id: number;

   set id(id: number) {
      this._id = id;
   }

   get id(){
        return this._id;
   }
}

Hero h = new Hero();
// Getter
var myId = h.id;

// Setter
h.id = 1;
```

### Mismo ejemplo sin Getters y Setters

```jsx
export class Hero {
   id: number;
}

Hero h = new Hero();
// Getter
const id = h.id;
// Setter
h.id = 2;
```

[TypeScript Getter & Setters](https://www.typescripttutorial.net/typescript-tutorial/typescript-getters-setters/)

### Herencia

```jsx
class Programador {
	readonly nombre: string;

	constructor(nombre: string) {
		this.nombre = nombre;
	}

	escribirCodigo() {
		return console.log(`${this.nombre} escribiendo codigo`);
	}

	tomarCafe() {
		return console.log('Esta tomando café');
	}
}

class ProgramadorWeb extends Programador {
	private readonly editorCodigo: string;

	constructor(nombre: string, editorCodigo: string) {
		//Siempre tener en cuenta llamar a las propiedades de la super clase
		super(nombre);
		this.editorCodigo = editorCodigo;
	}
	realizandoPaginaweb() {
		super.escribirCodigo();

		console.log(
			`${this.nombre} está realizando una pagina web con el editor ${this.editorCodigo}`,
		);
	}
}

const nombreDesarrollador = 'Fabian';
const editorCodigo = 'VsCode';

let desarrollandoVG = new ProgramadorWeb(nombreDesarrollador, editorCodigo);
desarrollandoVG.realizandoPaginaweb();
```

### Protected

Nos permite modificar y leer cualquier atributo si eres hijo de cualquier super clase

```jsx
class Programador {
	j

	constructor(nombre: string) {
		this.nombre = nombre;
	}
}

class ProgramadorWeb extends Programador {
	private editorCodigo: string;

	constructor(nombre: string, editorCodigo: string) {
		super(nombre);
		
		this.editorCodigo = editorCodigo;
	}
```

Permite modificar cualquier atributo de la super clase por fuera de ella, obviamente si una clase hija, como en el ejemplo anterior.

### Clases Abstractas

Son clases que no se pueden instanciar o inicializar, solamente se tiene acceso a ellas por las clases hijas como el siguiente ejemplo: 

```jsx
abstract class Programador {
	protected nombre: string;

	constructor(nombre: string) {
		this.nombre = nombre;
	}

	escribirCodigo() {
		return console.log(`${this.nombre} escribiendo codigo`);
	}
}

class ProgramadorWeb extends Programador {
	private editorCodigo: string;

	constructor(nombre: string, editorCodigo: string) {
		super(nombre);
		
		this.editorCodigo = editorCodigo;
	}
}
//Esto no se puede hacer porque es una clase abstracta
let desarrollandoVG = new Programador('Fabian');

// La manera correcta es inicializar desde la clase hija
let desarrolladoVG = new ProgramadorWeb('Fabian', 'Vscode');

```