# Alias

Cuando necesitamos varias veces un tipo de dato, para evitar repetir código lo mejor utilizar un alias

```jsx
type Punto = {
    x: number;
    y: number;
}

function imprimirCoordenada(punto: Punto) {
    console.log(`La coordenada x es : ${punto.x}`);
    console.log(`La coordenada y es : ${punto.y}`);
}

imprimirCoordenada({ x: 10, y: 25 });
```

En este ejemplo al utilizar un alias podemos proporcionar una lista de propiedades de las cuales consta el parámetro `punto`.

Para crear un alias usamos `type`, en este caso hemos creado un alías con dos propiedades tipo `number` pero esto no quiere decir que deban ser ambas iguales.