# Next

## Tabla de contenidos

- [1. ¿Qué es Next Js?](#1--que-es-next-js-)
- [2. ¿Por donde comenzar?](#2--por-donde-comenzar-)
  - [2.1 Instalación](#21-instalaci-n)
- [3. Carpetas y directorios](#3-carpetas-y-directorios)
- [4. Rutas](#4-rutas)
- [5. `Next/Link`](#5--next-link-)
- [6. Estilos dentro de los componentes `styled jsx`](#6-estilos-dentro-de-los-componentes--styled-jsx-)
- [7. Layouts](#7-layouts)
- [8. Typescript con Next](#8-typescript-con-next)
- [9. Desplegar en Docker con Next](#9-desplegar-en-docker-con-next)
- [Obtención de datos](#obtenci-n-de-datos)

## 1. ¿Que es Next Js?

Segun la pagina oficial Next es un Framework de React para aplicaciones multifunción, cuanta con una de las caracteristicas principales y la mas importante, [[Server Side Rendering]] muchas de las aplicaciones modernas tiene problemas con el posicionamiento, es decir para que los buscadores puedan encontarla, este framework soluciona parte de ambos problemas. Osea tendremos mejor rendimiento, SEO o posicionamiento en buscadores, enrutadores externos, etc.

## 2. ¿Por donde comenzar?

### 2.1 Instalación

En la web oficial de [Next](https://nextjs.org/docs/getting-started) el proceso de instalación que es muy sencillo, ya sea utilizando cualquiera de los gestores de paquetes yarn, npm o pnpm.
` yarn create next-app` o con typescript `yarn create next-app --typescript`.
Se puede también utilizar vite [[Instalación de Next con Vite]()].

## 3. Carpetas y directorios

Explicación de cada uno de los directorios y carpetas

Para mas información => **_[Carpetas y Directorios](002%20Carpetas%20y%20Directorios.md)_**

## 4. Rutas

Next cuenta con su propio enrutador, se tiene que instalar paquetes externos como en caso de React Router para aplicaciones SPA de React.

Para mas información => **_[Rutas en Next](005%20Rutas%20en%20Next.md)_**

## 5. `Next/Link`

Cuando queremos crear una ruta pero que no se recargue la pagina cada vez es decir un sistema (SPA) tenemos que indicarselo ya que por defecto con el router no está activado. Seria de la siguiente manera:

```jsx
import Link form 'next/link'

export const Home = () => {
	<Link href="/timeline"> Time Line</Link>
}
```

De esta forma será un link sin que se cargue nuevamente la pagina.

## 6. Estilos dentro de los componentes `styled jsx`

Dentro de los componentes de en Next se puede introducir estilos con la siguiente etiqueta:

```jsx
<style jsx>{`... Todos lo estilos`} </style>`
```

Para mas información: **_[Estilos dentro de los componentes](004%20Estilos%20dentro%20de%20los%20componentes.md)_**

## 7. Layouts

Los layouts o plantillas son paginas o componentes que se repiten dentro de nuestra aplicación.

Para mas información: **_[Layouts](006%20Layouts.md)_**

## 8. Typescript con Next

Guía para migrar proyectos de javascript a typescript

**_[Next con Typescript](007%20Next%20con%20Typescript.md)_**

## 9. Desplegar en Docker con Next

Paso a paso de como levantar imagen con Docker

Para mas información: [Desplegar Next con Docker](009%20Desplegar%20Next%20con%20Docker.md)

## Obtención de datos

- [[getInitialProps]] : Añade al servidor los props que va utilizar el componente. Muy importante para el CEO.

###### Tags: #next #react
