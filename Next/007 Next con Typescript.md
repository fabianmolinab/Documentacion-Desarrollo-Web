# Next con Typescript

## Instalaciones

### Crear `tsconfig.json`

1. En la terminal:  `touch tsconfig.json`
2. `npm install --save -dev typescript @types/react @types/node` 
	 `yarn add --dev typescript @types/react @types/node`
3.  Opcional: crear sino fue creado `next-env-d-ts` 

### De `_app.js`  a `_app.tsx`

```tsx
import { AppProps } from 'next/app';

function App({ Component, pageProps }: AppProps) {
  return <Component {...pageProps} />;
}

export default App;
```

### Layouts Props `children`

Con react 18 definimos las props children como *React.ReactNode*, como en siguiente ejemplo:

```tsx
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
    </div>  
```

