# Configuración de Eslint con Next

### Instalamos ESLINT

` npm install eslint -D` o `yarn add eslint -D`

### Configuramos `EsLint`

`npx eslint --init` => Inicializamos el paquete

Configuramos según la reglas mas populares, en mi caso recomendamos la de StandardJS :)

### Archivo de configuración `eslintrc`

Para NEXT sin Typescript y Standard: 

```json
{
    "env": {
        "browser": true,
        "es2021": true,
        "node": true
    },
    "extends": [
        "plugin:react/recommended",
        "standard"
    ],
    "parserOptions": {
        "ecmaFeatures": {
            "jsx": true
        },
        "ecmaVersion": "latest",
        "sourceType": "module"
    },
    "plugins": [
        "react"
    ],
    "rules": {
      "react/react-in-jsx-scope": "off",
      "space-before-function-paren": "off"
    },
    "settings": {
      "react": {
        "version": "latest"
      }
    }
}
```

### Agregamos en package.json

```json
"scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "elint": "eslint --fix ."
  },
```