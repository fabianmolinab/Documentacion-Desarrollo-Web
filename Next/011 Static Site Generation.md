
# Generación estatica `(getStaticProps)`

Next tiene distintas formas de servir información, puede ser Server Side Render (SSR), Generación estatica (SSG) o Generación Estatica Incremental (SIG). 

La *generacion estatica* se usa cuando conocemos los datos que nuestra pagina necesita y no cambian en tiempo real. Cuando se crea la pagina o hace la primera petición al servidor no necesita realizar mas por que los datos ya vienen precargados del lado del servidor. 
Util en casos de una landing page o tiendas virtuales de catálogos estrictos donde la información no varia en la base de datos.

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


[Documentación Oficial](https://nextjs.org/docs/basic-features/data-fetching/get-static-props)

**Artículos sugeridos**
[Server Side Rendering](./Server%20Side%20Rendering.md)