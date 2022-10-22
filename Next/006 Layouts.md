# Layouts

Son componentes reutilizables listos para usar en cualquier pagina. 

## Primeros pasos

En ***components/layouts/*** es donde estarán ubicados todos estos componentes, *MainLayout.tsx* sería un ejemplo de como nombrarlos.

```tsx
//MainLayout.tsx
import React from 'react'
import Head from 'next/head'
import { Navbar } from '../Navbar'
import styles from './Main.module.css'

interface Props {
  children: React.ReactNode
  }

export const MainLayout: React.FC<Props> = ({ children }) => {
  return (
    <div className={styles.container}>
      <Head>
        <title>Home Page</title>
        <meta name="Pagina Home" content="Estoy aprendiendo Next" />
        <link rel="icon" href="/favicon.ico" />
      </Head>

    <Navbar />
      <main className={styles.main}>
      {children}
     </main>
    </div>
  )
}
```

Llamamos el componente de la siguiente manera:

```tsx
//page/inde.tsx
import Link from 'next/link'
import { MainLayout } from '../components/layouts/MainLayout'

const Home: React.FC = () => {
  return (
      <MainLayout>
        <h1 className={'title'}>Este es el Home</h1>
        <hr/>
        <h1 className={'title'}>
          Ir a <Link href="/about">about</Link>
        </h1>
      </MainLayout>
  )
}
export default Home
```