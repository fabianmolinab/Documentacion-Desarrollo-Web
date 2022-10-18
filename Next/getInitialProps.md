# getInitialProps

Añade las props del lado del servidor que va utilizar el componente. La documentación oficial [getInitialProps](https://nextjs.org/docs/api-reference/data-fetching/get-initial-props) .

### Ejemplo

```tsx
import { NextPage } from 'next'
import Link from 'next/link'
import styles from '../../styles/Home.module.css'

interface Props {
  username: string
}

const TimeLine: NextPage<Props> = ({ username }) => {
  return (
    <>
      <h1>Time Line is {username}</h1>
      <p>Aqui van los tuits</p>
      <Link href="/" >
        <a className={styles.title}>Home</a>
      </Link>
    </>
  )
}
// Añade al servidor las props que va utilizar el componente
TimeLine.getInitialProps = () => {
  return { username: '@fabianmolinab' }
}

export default TimeLine
```

En este ejemplo le pasamos *username* que la prop que renderiza el componente. Algo muy importante es que todos los métodos que pasamos por esta función son asíncronos, así que podemos pasar promesas o async y await. Dentro de la documentación afirman que esta función esta siendo deprecada por métodos mas actuales para traer datos a los componentes.

**Nota:** Las getInitialProps solo se pueden utilizar en paginas, nada de jsx ni componentes funcionales. 