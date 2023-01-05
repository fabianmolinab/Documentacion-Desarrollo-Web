# Test en React con Jest y Testing Library

## Configuraciones

Sigue los pasos de la [Documentación oficial]() de configurar Jest y React Testing Library

Son las pruebas que se le haces a cada componente de la aplicación para que todo funcione correctamente

## Características

1.  Fáciles de escribir
2.  Fáciles de leer
3.  Confiables
4.  Rápidas
5.  Principalmente unitarias

## Estructurar el directorio de pruebas

Para realizar los test se deben alojar en el directorio con nombre **tests** o **test .** A su vez cada archivo de pruebas debe llevar un nombre descriptivo acompañado de `.test.js`. Un ejemplo seria `demo.test.js`.

Algo muy importante es que el directorio de pruebas debe ser iguales al directorio de desarrollo para no generar confusiones, es decir debe llevar la misma estructura de carpetas y archivos.

## Sintaxis de las pruebas

Para realizar las pruebas se empieza inicializando la función `test()`que tiene como parámetros **descripción** y como se podrá ver en el siguiente ejemplo:

```jsx
test('deben de ser iguales los strings', () => {

    // 1. inicialización
    const mensaje = 'Hola mundo';

    // 2. estimulo
    const mensaje2 = `Hola mundo`;

    // 3. Observar el comportamiento

    expect(mensaje).toBe(mensaje2); // ===

  })
```

En el ejemplo anterior vemos la estructura de una prueba **`test` .** En el parámetro inicial tenemos una descripción de la prueba, lo siguiente es una función tipo flecha con el contenido de la prueba; vemos tanto la **Iniciación, estimulo y comportamiento;** que son las estructuras básicas de una prueba. En `expect` se esta validando con `toBe` si ambos strings son iguales, es igual a realizar una comparación con if.

Con `testing-library` seria de la siguiente manera:
```jsx
import MyComponent from './MyComponent';
import { render, fireEvent } from '@testing-library/react';

test('MyComponent renders the correct greeting', () => {
  // Preparar los datos de prueba
  const name = 'Alice';

  // Renderizar el componente
  const { getByText } = render(<MyComponent name={name} />);

  // Hacer la comprobación
  const greeting = getByText(`Hello ${name}!`);
  expect(greeting).toBeInTheDocument();
});
```


## `expect`

La función `expect` se utiliza cada vez que desea testear un valor. Rara vez se utiliza `expect` por sí mismo. En su lugar, utilizarás `expect` junto a una función de "comparación" para afirmar algo sobre un valor. Esta función tiene diferentes métodos.

## Métodos `expect` mas importantes

### `toBe`

Utilice `.toBe` para comparar valores primitivos o para verificar la identidad referencial de instancias de objetos. Llama a [`Object.is`](http://object.is/) para comparar valores, que es incluso mejor para las pruebas === operador de igualdad estricta.

**Ejemplo:**

```jsx
const lata = {
  nombre: 'pomelo',
  onzas : 12,
};

describe('la lata', () => {
  test('tiene 12 onzas', () => {
    expect(lata.onzas).toBe(12);
  });

  test('tiene un nombre sofisticado', () => {
    expect(lata.nombre).toBe('pomelo');
  });
});
```

## `toEqual`

Se utiliza para comparar objetos, analiza que cada una de las propiedades y valores de los objetos sean iguales.

## Estructura de carpetas 




## Enlaces
[Testing](000%20Testing.md)