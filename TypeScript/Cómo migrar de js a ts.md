# Cómo migrar de forma sencilla de JavaScript a TypeScript

Fechas: October 10, 2021 9:58 AM

Es mucho más sencillo abandonar JS al empezar un proyecto nuevo, cuando no te tienes que preocupar por la retro-compatibilidad, el mantenimiento de la app en producción o cosas por el estilo. En este caso puedes probar algunas de las muchas alternativas y quedarte con la que más te guste.

Sin embargo, si debes seguir trabajando con un proyecto antiguo puedes empezar la **migración de JavaScript a TypeScript** de forma “lenta” (archivo a archivo), o añadiendo TypeScript únicamente en los nuevos archivos que crees.

Esto es posible debido a que TypeScript es un superconjunto de JavaScript, es decir, cualquier código de JS es también válido en TS (siempre y cuando TS esté configurado para ser compatible).

A continuación os mostraré una forma sencilla de añadir TypeScript a un proyecto sin necesidad de modificar la configuración de webpack, gulp o sea cual sea el sistema de build, ni de deploy el sistema.

Asumiendo que usas npm como package manager en tu proyecto, lo primero que debemos hacer es añadir TypeScript como dependencia (si no, lo puedes instalar de forma global).

```
npm install --save-dev typescript
```

Nota: dependiendo de tu proyecto, quizás deberías instalar “@types” para aquellas librerías en las que tengas dependencias; por ejemplo, si tu proyecto es react-redux, te interesaría instalar estos elementos:

```tsx
npm install --save-dev @types/node
npm install --save-dev @types/react
npm install --save-dev @types/react-dom
npm install --save-dev @types/react-redux
npm install --save-dev @types/react-router-dom
```

Después debemos añadir un archivo “tsconfig.json” al directorio raíz del proyecto. Este archivo contiene las opciones de compilador necesarias para convertir TS en JS. Para tener el menor número de problemas posible, usa la siguiente configuración para hacer JS compatible con el código de TS:

```
{
 "compilerOptions": {
     "module": "commonjs",
     "sourceMap": true,
     "jsx": "react"
 },
 "exclude": [
     "node_modules"
 ]
}
```

Nota: Quizás deberás cambiar algunos elementos según tu proyecto. Más información [aquí](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html).

Ahora, añade este script en tu package.json:

```
"tsc:w": "tsc -w"
```

Y ejecútalo. Activará un observador que transpilará todos los archivos .ts (o .tsx) en archivos .js normales. Además, generará estos archivos en el mismo path que los originales, así que todos los imports y procesos de build que tengas seguirán funcionando igual hasta ahora, pues los archivos .ts son totalmente ignorados y en su lugar se usan los resultados de la transpilación. La estructura de los archivos generados es la siguiente:

```
file.ts
 ├── file.js
 └── file.js.map
```

Ahora, todo lo que debemos hacer es crear nuestro primer archivo “.ts” cambiando la extensión de uno ya existente que queramos migrar a TypeScript, o crear un nuevo archivo donde empezar a trabajar en nuestra aplicación.

Igualmente, este cambio no aporta demasiadas variaciones. Aún podemos utilizar código JS normaly no tener acceso a ninguna de las funcionalidades de TypeScript. Para que TS nos fuerce a typear nuestro código debemos cambiar el archivo “tsconfig.json”. En concreto, nos centraremos en dos opciones de compilador que forzarán nuestro código a ser *typeado*:

```
"noImplicitAny": true,
"strictNullChecks": true,
```

Imaginemos que tenemos un simulador de hipotecas sencillo, que le dice al usuario si, dada su situación financiera, una hipoteca es viable o no. Para este fin, tenemos una función que devuelve como valor los ahorros del usuario:

```
function getSavings() {
 //returns savings
 }
```

Y una función para decidir si la hipoteca es viable:

```tsx
function concedeMortgage(homeValue) {
     const savings = getSavings();
     return savings / homeValue > 0.2;
}
```

Pero para que funcione, primero debemos comprobar que el este dato existe, así como si es un número o no. Lo mismo para el valor que debe devolver la función “getSavings”, pues no sabemos qué tipo de *return* nos dará. Teniendo todo esto en cuenta, nuestro código podría parecerse a algo así:

```tsx
function concedeMortgage(homeValue) {
     if(!homeValue || !parseFloat(homeValue)) return false;
     const savings = getSavings();
     if(!savings || !parseFloat(savings)) return false;
     return savings / homeValue > 0.2;
}
```

Y esto tiene una pinta horrible.

Pero, si activamos la opción de compilador “noImplicitAny”, ya no será necesario comprobar si el valor del input y el return de “getSavings” es de tipo número, así que la función ahora se vería así:

```tsx
function concedeMortgage(homeValue: number): boolean {
     if(!homeValue) return false;
     const savings = getSavings();
     if(!savings) return false;
     return savings / homeValue > 0.2;
}
```

Lo cual es una mejora, pues el compilador nos ayudaría a evitar errores potenciales de sintaxis, por ejemplo, no permitiéndonos llamar la función mediante un string:

```
concedeMortgage("foo")  // ERROR! Argument of type 'foo' is not assignable to parameter type 'number'

```

Por desgracia, los valores *null* y *undefined* están presentes en todos los tipos de input, así que esta situación aún podría pasar:

```
concedeMortgage(null) // Still works
```

Para solventar esto, deberemos activar otra opción en el archivo tsconfig.json: ‘strictNullChecks’.

Ahora, si llamamos la función con un *null*, el compilador se dará cuenta:

```
concedeMortgage(null) // ERROR! Argument of type 'null' is not assignable to parameter of type 'number'
```

Lo que esto significa es que deja de ser necesario el comprobar los valores de los inputs mediante código, simplificando la lógica hasta dejarla más o menos así:

```
function concedeMortgage(homeValue: number): boolean {
     const savings = getSavings();
     return savings / homeValue > 0.2;
}
```

Y esto es solo un pequeño ejemplo de los beneficios que TypeScript te puede aportar si decides migrar tu proyecto de JS a TS.

More to Explore

- [Estudio sobre la situación actual del Software](https://apiumhub.com/es/tech-blog-barcelona/situacion-actual-del-software/)
- [Apiumhub, entre los principales líderes del sector…](https://apiumhub.com/es/tech-blog-barcelona/apiumhub-entre-los-principales-lideres-del-sector-it-en-el-evento-code-europe/)
- [Razones por las que Scala sigue ganando popularidad](https://apiumhub.com/es/tech-blog-barcelona/lenguaje-scala/)
- [25 Mujeres Influyentes del Desarrollo de Software](https://apiumhub.com/es/tech-blog-barcelona/25-mujeres-influyentes-desarrollo-software/)
- [Método Kanban: principios y ventajas](https://apiumhub.com/es/tech-blog-barcelona/metodo-kanban-ventajas/)
- [Beneficios de las feature toggles o feature flags](https://apiumhub.com/es/tech-blog-barcelona/beneficios-feature-toggles-feature-flags/)
- [Construye un bot con el nuevo Bot Framework Composer](https://apiumhub.com/es/tech-blog-barcelona/construye-un-bot-con-el-nuevo-bot-framework-composer/)
- [Arquitectura de sacrificio](https://apiumhub.com/es/tech-blog-barcelona/arquitectura-de-sacrificio/)
- [Cómo crear un proyecto React con TypeScript](https://apiumhub.com/es/tech-blog-barcelona/como-crear-proyecto-react-typescript/)