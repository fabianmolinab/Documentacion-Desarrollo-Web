
# Generación estatica `(getStaticProps)`

Next tiene distintas formas de servir información, puede ser Server Side Render (SSR), Generación estática (SSG) o Generación Estatica Incremental (SIG). [getStaticProps](https://nextjs.org/docs/basic-features/data-fetching/get-static-props) 

La *generacion estatica* se usa cuando conocemos los datos que nuestra pagina necesita y no cambian en tiempo real. Cuando se crea la pagina o hace la primera petición al servidor no necesita realizar mas por que los datos ya vienen precargados del lado del servidor. 

Útil en casos de una landing page o tiendas virtuales de catálogos estrictos donde la información no varia en la base de datos.

## Ejemplos

```jsx

function Blog({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li>{post.title}</li>
      ))}
    </ul>
  )
}

// Esta función llama en tiempo de ejecución del lado del servidor.
export async function getStaticProps() {
  // Llama a una API externa por medio de endpoints.
  // Se usa una libreria de fetch
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  // Retorna { props: { posts } }, en el componente blog
  // por medio de las props
  return {
    props: {
      posts,
    },
  }
}
export default Blog
```

## Static side generation con argumentos

### Rutas Dinámicas

Se utiliza para rutas dinámicas, un ejemplo sería los post dentro de un blog con múltiples entradas, cada post tiene una ruta que puede venir de una base de datos o un CMS.

Para crear las Rutas tenemos [useRouter](https://nextjs.org/docs/api-reference/next/router#userouter) es un hook que contiene un objeto que muestra mucha información sobre el manejo de la rutas. 

#### Ejemplo

- Navegando a una ruta predeterminada: `pages/about.js`
```jsx
import { useRouter } from 'next/router'

export default function Page() {
  const router = useRouter()

  return (
    <button type="button" onClick={() => router.push('/about')}>
      Click me
    </button>
  )
}
```

- Navegando a una ruta dinámica: `pages/post/[id].jsx`
```jsx
import { useRouter } from 'next/router'

export default function Page({id}) {
  const router = useRouter()
  const onClick= () => {
    router.push(`/post/${id}`)
  }
  return (
    <button type="button" onClick={onClick}>
      Click me
    </button>
  )
}
```

>Nota: para este ejemplo se debe crear una pagina de con el mismo nombre de la ruta en este caso seria en ´pages/post/[id].jsx´

### getStaticPaths 

En Next.js, la función `getStaticPaths` es una función especial que se puede exportar desde un archivo de página y que **se usa para generar rutas dinámicas estáticas**. Esto es útil cuando quieres crear una página que muestre contenido para diferentes valores de parámetros de ruta, pero todo el contenido se puede generar de manera estática durante la fase de build.

Por ejemplo, imagine que quieres crear una página de detalles de producto que muestre información sobre diferentes productos. Puedes usar `getStaticPaths` para generar una ruta para cada producto disponible en tu base de datos, de manera que el usuario pueda acceder a la página de detalles de cada producto con una URL como `/products/[id]`, donde `[id]` es el ID del producto.

Por ejemplo, si estás usando una base de datos, podrías hacer una consulta a la base de datos para obtener una lista de IDs de productos:

```jsx
export async function getStaticPaths() {
  const db = await connectToDatabase();
  const productIds = await db.query('SELECT id FROM products');

  return {
    paths: productIds.map(product => `/products/${product.id}`),
    fallback: false,
  };
}
```

### Ejemplos

[Ejemplo en aplicación real de getStaticPaths](https://github.com/fabianmolinab/pokemon-static-page/blob/fdf91772df263562611befe809cf1b8bdd532cb3/pages/pokemon/%5Bid%5D.tsx#L19) 

## Artículos sugeridos

[Server Side Rendering](./Server%20Side%20Rendering.md)

