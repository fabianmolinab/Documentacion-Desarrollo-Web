# TypeScript con React

Fechas: December 31, 2021 2:46 PM
Tipos: Clase

## Interfaces para Tipar Componentes

Uno de los propósitos para utilizar TypeScript con React es para tipar componentes y evitar errores y documentar mucho mejor nuestro código, para esto las interfaces nos ayudan a definir los tipos de datos que requiere el componente para existir, como por ejemplo:

```tsx
interface Props {
  title: string;
  subtitle: string;
}

export const App = ({ title, subtitle }: Props) => {
  return (
    <>
      <h1>Fabian es: {title}</h1>
      <p>Es el mejor de todos los {subtitle}</p>
    </>
  )
}
```

Estoy definiendo como `**interface**` **Props** se pase como argumento de la función, que este caso sea title, subtitle, ambos son propiedades que requiere el componente para existir, que son de tipo Props que esta estructurado como un objeto, por lo siguiente se desestructura con `**({ title, subtitle }: Props)**`  y ya tenemos las propiedades disponibles y deben ser siempre mandadas con el tipo de dato de la inteface. 

## Interfaces de estados de React

- Inicializamos el useState

![](./Imagenes/React-type1.png)

Para tipar la inicialización del useState, se definió el tipo de dato por medio de una **interface** con los parametros del objeto. Con **<Tareas>** definimos el parametro de la función `useState` con la interface 

- Pasamos los datos del estado por las props y hacemos el interface

![](./Imagenes/React-type2.png)

Aca vemos **un interface de un useState de React** donde el useTask es una función que maneja el estado, ya definimos Tareas en el paso anterior y ahora lo llamamos para que tenga los mismos datos del inicio, asi podemos definir todo el objeto para que se cambie al pasar las props.

## Tipar eventos de los componentes

Acá tenemos un componente que contiene un formulario con input y  text area respectivamente

![](./Imagenes/React-type3.png)

El **`handleChange`** es el evento que va leer el value del input y textarea, entonces podemos tipar para que el evento solo se ejecute en uno o varios elementos del DOM. En este caso se realizó un type llamando `**ChangeEvent**` que nos permite definir el tipo de elementos que podran ejecutar este evento que en esta caso es un función, que se ejecuta cada vez que se cambia el input.


### Referencias
[[React Typescript Basics]] *Buenas practicas de Typescript con React*