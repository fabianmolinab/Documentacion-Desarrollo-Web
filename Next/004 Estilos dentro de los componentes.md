# Estilos dentro de los componentes

1. Dentro de los componentes de en Next se puede introducir estilos con la siguiente etiqueta:

```jsx
<style jsx>{`... Todos lo estilos`} </style>`
```

2. Otra formar de usar estilos es con js de la siguiente manera: 

```js
export const ActiveLink = ({ content, link }) => {
  const { asPath } = useRouter()

  return (
    <Link href={link}>
      <a style={asPath === link ? style : null }>{content}</a>
    </Link>
  )
}
const style = {
  color: '#0070f3',
  textDecoration: 'underline'
}
```
En este código podemos ver como se importan los estilos a una etiqueta con *style={}* dentro se sirve el código en forma de array.

3. La ultima forma es implementar el código de css en módulos, seria renombrando nuestros archivos *Navbar.module.css* y pasarlo como className dentro de cualquier etiqueta

```js
import styles from './Navbar.module.css'

import { ActiveLink } from './ActiveLink'

export const Navbar = () => {
  return (
      <nav className={styles['menu-container']}>
        <ActiveLink link="/" content="Home" />
      </nav>
  )
}
```

Estas son todas las formas importar y usar css en nuestras aplicaciones con Next sin bibliotecas o framework externos pero se puede usar cualquiera de estos dado el caso que quiera usar, ya sea style components, tailwind, emotion, etc.

## ¿Como colocar estilos globales?

- La primera forma se implementa con los estilos dentro de los componentes como en el ejemplo anterior pero añadiendo el atributo **global,** seria la siguiente manera:
	
	`<style jsx global>{``}</style>`
	
- Desde *_app.ts* o *_app.js* podemos importar los estilos globales desde otro archivo con los estilos.  Creamos el archivo *styles/globals.css* y luego lo importamos en *_app.ts.* Esta es la forma recomendada. 


###### Tags: #next #react #estilos 