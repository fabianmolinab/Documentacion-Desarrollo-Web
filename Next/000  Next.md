# Next

## ¿Qué es Next Js

Segun la pagina oficial Next es un Framework de React para aplicaciones multifunción, cuanta con una de las caracteristicas principales y la mas importante, [[Server Side Rendering]] muchas de las aplicaciones modernas tiene problemas con el posicionamiento, es decir para que los buscadores puedan encontarla, este framework soluciona parte de ambos problemas. Osea tendremos mejor rendimiento, SEO o posicionamiento en buscadores, enrutadores externos, etc.

## ¿Por donde comenzar?

### Instalación

En la web oficial de [Next](https://nextjs.org/docs/getting-started) el proceso de instalación que es muy sencillo, ya sea utilizando cualquiera de los gestores de paquetes yarn, npm o pnpm.
` yarn create next-app` o con typescript `yarn create next-app --typescript`.
Se puede tambien utilizar vite [[Instalación de Next con Vite]].

## Rutas

Como ya saben Next cuenta con su propio enrutador, se tiene que instalar paquetes externos como en caso de React Router para aplicaciones SPA de React. 

Para mas información => [[003 Rutas en Next]]


## Estilos dentro de los componentes `styled jsx`

Dentro de los componentes de en Next se puede introducir estilos con la siguiente etiqueta:

```jsx
<style jsx>{`... Todos lo estilos`} </style>`
```

Para mas información: [[004 Estilos dentro de los componentes]] 

## Obtención de datos

- [[getInitialProps]] : Añade al servidor los props que va utilizar el componente. Muy importante para el CEO. 



###### Tags: #next #react 