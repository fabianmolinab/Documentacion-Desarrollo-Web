**BEM** es una convención o metodología para nombrar tus clases de CSS. Por sus siglas en inglés, BEM significa **B**loque, **E**lemento y **M**odificador.

En esta guía aprenderemos:

-   Cómo funciona BEM
-   Cómo usar BEM en CSS
-   Por qué y para qué usar BEM
-   Ejemplo prácticos de BEM (incluyendo un cohete Falcon 9 de Space X) 🚀
-   3 casos con lo que debes y no debes hacer con BEM
-   3 problemas comunes en BEM y cómo solucionarlos
-   BEM + SASS
-   Recomendaciones finales

![](https://i.ibb.co/WsSq3y3/2.png)

## ¿Cómo funciona BEM?

BEM funciona identificando el bloque, el elemento y el modificador de un componente.

-   **Bloque** es el contenedor principal del componente.
-   **Elemento** son las partes internas que conforman el componente.
-   **Modificador** son las variaciones del bloque o del elemento.

El cohete Falcon 9 de SpaceX está compuesto por varias partes que hacen posible el transporte confiable y seguro de personas o cargas útiles a la órbita terrestre (incluso más allá). Para cada una de las partes podemos crear una analogía.

Vamos a identificar quién sería el elemento bloque, quiénes serían los elementos y quiénes serían los modificadores, así:

![](https://i.ibb.co/PDGcrSc/1.png)

Teniendo entonces:

-   **Bloque:** Falcon 9
-   **Elementos:** First stage, Interstage, Second stage.
-   **Modificador:** Fairing, Dragon.

Después de revisar la analogía con el cohete Falcon 9, revisemos algunos ejemplos que podemos encontrarnos en la vida real:

-   **Bloque:** card, button, form, menu, header…
-   **Elemento:** icon, text, item, image, input, button…
-   **Modificador:** active, big, right, secondary, red…

😍

### Cómo se usar BEM en CSS

Los nombres de clases con convención BEM,pueden tener la siguiente sintaxis:

-   `[bloque]`
-   `[bloque]__[elemento]`
-   `[bloque]--[modificador]`
-   `[elemento]--[modificador]`
-   `[bloque]__[elemento]--[modificador]`

Teniendo en cuenta lo anterior, el CSS para nuestro Falcon 9 se escribiría así:

-   `.falcon9 { ... }`
-   `.falcon9--fairing { ... }`
-   `.falcon9--dragon { ... }`
-   `.falcon9__first-stage { ... }`
-   `.falcon9__interstage { ... }`
-   `.falcon9__second-stage { ... }`

Y así se vería el HTML:

```
<rocket class="falcon9 falcon9--dragon">
    <stage class="falcon9__first-stage"></stage>
    <stage class="falcon9__interstage"></stage>
    <stage class="falcon9__second-stage"></stage>
</rocket>
```

Además, el CSS siguiendo BEM con un ejemplo de la vida real se escribiría así:

-   `.button { ... }`
-   `.button--active { ... }`
-   `.button__icon { ... }`
-   `.button__text { ... }`

Y así se vería el HTML:

```
<button class="button button--active">
    <i class="button__icon"></i>
    <span class="button__text"></span>
</button>
```

⚠️ Importante: recuerda que:

-   Los guiones bajos (`__`) se usan para separar el bloque del elemento,
-   Los guiones medios (`--`) se usan para separar el bloque o el elemento del modificador.

> 💡 Nota: BEM permite cambiar esta nomenclatura. También puedes encontrar nombres de clase así: `[bloque]__[elemento]-[modificador]`, `[bloque]__[elemento]_[modificador]`, entre otros. Lo más importante a la hora de usar una de estas nomenclaturas es ser consistente en todo el proyecto.

### ¿Por qué y para qué usar BEM?

Tal vez te preguntes, “Pero, ¿Teff, para qué seguir esta metodología si el resultado en CSS es el mismo? ¡Solo estamos haciendo más trabajo!”

1.  Para tener un CSS más fácil de leer, entender, mantener y escalar.
2.  Para organizar las clases de CSS en módulos independientes.
3.  Para evitar selectores de CSS anidados.

## Casos prácticos de BEM

### Card:

Identifiquemos el bloque, los elementos y los modificadores (si los tiene) de la siguiente card:

![](https://i.ibb.co/448DQ5g/3.png)

De la imagen anterior, tenemos lo siguiente:

-   **Bloque:** card
-   **Elementos:** image, text
-   **Modificadores:** (no tiene)

Su estructura de HTML con la convención de clases BEM, sería:

```
<div class="card">
    <img class="card__image" src="/image.png" alt="spacesuit" />
    <p class="card__text"></p>
    <p class="card__text"></p>
</div>
```

### Navbar:

Identifiquemos el bloque, los elementos y los modificadores (si los tiene) del siguiente navbar:

![](https://i.ibb.co/1z0x2Sr/4-1.png)

De la imagen anterior, tenemos lo siguiente:

-   **Bloque:** navbar
-   **Elementos:** logo, items
-   **Modificadores:** gray

Su estructura de HTML con la convención de clases BEM, sería:

```
<nav class="navbar">
    <ul class="navbar">
        <li class="navbar__item"><i class="navbar__icon"></i></li>
        <li class="navbar__item">MENS</li>
        <li class="navbar__item">WOMENS</li>
        <li class="navbar__item">KIDS</li>
        <li class="navbar__item">ACCESSORIES</li>
        <li class="navbar__item">PREMIUM</li>
        <li class="navbar__item navbar__item--gray">ACCOUNT</li>
        <li class="navbar__item navbar__item--gray">SEARCH</li>
        <li class="navbar__item">CART (0)</li>
    </ul>
</nav>
```

### Section:

Identifiquemos el bloque, los elementos y los modificadores (si los tiene) de la siguiente sección:

![](https://i.ibb.co/ssgY8Pf/5.png)

Como de la imagen anterior identificamos 2 bloques, vamos a dividir la estructura en 2 partes, así:

Para el bloque 1:

-   **Bloque:** section
-   **Elementos:** text, image
-   **Modificadores:** primary, secondary-semibold, secondary-bold

Para el bloque 2:

-   **Bloque:** list
-   **Elementos:** item, text
-   **Modificadores:** gray

La estructura de HTML con la convención de clases BEM para ambos bloques, sería:

```
<section class="section">
    <div>
        <h2 class="section__text section__text--primary">FALCON 9</h2>
        <p class="section__text section__text--secondary-semibold">Falcon 9, the world's first orbital class reusable rocket...</p>
        <p class="section__text section__text--secondary-bold">Learn more about Falcon 9</p>
        <ul class="list">
            <li class="list__item">
                <span class="list__text">VEHICLE HEIGHT</span>
                <div>
                    <span class="list__text">70m</span>
                    <span class="list__text list__text--gray">/229.6 ft</span>
                </div>
            </li>
            <li class="list__item">
                <span class="list__text">VEHICLE DIAMETER</span>
                <div>
                    <span class="list__text">3.7m</span>
                    <span class="list__text list__text--gray">/12 ft</span>
                </div>
            </li>
            <li class="list__item">
                <span class="list__text">FAIRING HEIGHT</span>
                <div>
                    <span class="list__text">13.1m</span>
                    <span class="list__text list__text--gray">/43 ft</span>
                </div>
            </li>
            <li class="list__item">
                <span class="list__text">FAIRING DIAMETER</span>
                <div>
                    <span class="list__text">5.2m</span>
                    <span class="list__text list__text--gray">/17.1 ft</span>
                </div>
            </li>
        </ul>
    </div>
    <div>
    </div>
    
</section>
```

## Casos con lo que debes y no debes hacer con BEM

### 1️⃣ Primer caso

-   **Lo que sí:** dejar la clase principal `card` y añadir otra clase con modificador.

```
<div class="card card--flat"></div>
```

-   **Lo que no:** usar la clase con modificador como clase principal.

```
<div class="card--flat"></div>
```

### 2️⃣ Segundo caso

-   **Lo que sí:** no representar los niveles de profundidad de HTML con BEM.

```
<div class="card">
    <img class="card__image" src="/image.png" alt="Crew Dragon" />
    <p class="card__text">
        <i class="card__icon">
    </p>
</div>
```

-   **Lo que no:** representar los niveles de profundidad de HTML con BEM.

```
<div class="card">
    <img class="card__image" src="/image.png" alt="Crew Dragon" />
    <p class="card__text">
        <i class="card__text__icon">
    </p>
</div>
```

### 3️⃣ Tercer caso

-   **Lo que sí:** incluir la clase en un hijo que necesita estilos.

```
<div class="card">
    <img class="card__image" src="/image.png" alt="Crew Dragon" />
</div>

<style>
    .card { ... }
    .card__image { ... }
</style>
```

-   **Lo que no:** Omitir la clase en un hijo que necesita estilos.

```
<div class="card">
    <img src="/image.png" alt="Crew Dragon" />
</div>

<style>
    .card { ... }
    .card img { ... }
</style>
```

## 3 problemas comunes con BEM y cómo solucionarlos

### 1️⃣ Primer caso

-   **Problema:** tengo un componente A que ya tiene sus propias clases y deseo añadirlo a un nuevo componente B. ¿Debo agregar una nueva convención para el componente A que estará dentro de B?

Componente A:

```
<button class="button button--active"></button>
```

Componente B:

```
<div class="card">
    <img class="card__image" src="/image.png" alt="Crew Dragon" />
</div>
```

-   **Solución:** puedes dejar el componente A con las clases que ya estaban establecidas así no sean coherentes con el nuevo componente B, por ejemplo:

```
<div class="card">
    <img class="card__image" src="/image.png" alt="Crew Dragon" />
    <button class="button button--active"></button>
</div>
```

### 2️⃣ Segundo caso

-   **Problema:** en mi estructura de HTML tengo padres, hijos, nietos, tataranietos, etc; pero BEM sólo me deja usar 3 niveles. ¿Qué hago con los elementos nietos y sus descendientes?

```
<div class="card">
    <img class="card__image" src="/image.png" alt="Crew Dragon" />
    <div class="card__footer">
        <p class="card__footer__text">
            <i class="card__footer__text__icon">
        <p>
    </div>
</div>
```

-   **Solución:** como lo mencionamos anteriormente, BEM no representa los niveles de tu estructura de HTML. Lo ideal en este caso sería tener:

```
<div class="card">
    <img class="card__image" src="/image.png" alt="Crew Dragon" />
    <div class="card__footer">
        <p class="card__text">
            <i class="card__icon">
        <p>
    </div>
</div>
```

### 3️⃣ Tercer caso

-   **Problema:** quiero utilizar la propiedad `display: none` para ocultar desde JavaScript un componente de Card y un componente de Botón. ¿Debo crear una clase para cada componente siguiendo su propia estructura de BEM (`card--hidden` y `button--hidden`)?

```
<div class="card card--hidden">
    <img class="card__image" src="/image.png" alt="Crew Dragon" />
</div>
<button class="button button--hidden"></button>

<style>
    .card--hidden {
        display: none;
    }
    .button--hidden {
        display: none;
    }
</style>
```

-   **Solución:** puedes crear una clase independiente a la estructura de BEM para aplicar propiedades generales, así, reducirás la cantidad de líneas de JavaScript ya que no tendrás que usar una clase específica para cada componente.

```
<div class="card hidden">
    <img class="card__image" src="/image.png" alt="Crew Dragon" />
</div>
<button class="button hidden"></button>

<style>
    .hidden {
        display: none;
    }
</style>
```

## • BEM + SASS

Dragon es la primera nave espacial privada en llevar humanos a la estación espacial. Pero, no lo hace sola. Dragon trabaja en conjunto con el cohete Falcon 9 para tener un lanzamiento perfecto.

![](https://i.ibb.co/SVMGRkH/Screen-Shot-2021-04-29-at-2-02-48-AM.png)

Así como Dragon y Falcon 9 trabajan juntos, BEM y SASS también. SASS es un preprocesador de CSS que te permite anidar selectores, crear bucles, funciones, entre otras cosas. Y, adicionalmente, gracias a la sintaxis de SASS, podemos tener una combinación perfecta en nuestras hojas de estilos.

Por ejemplo, uno de nuestros ejercicios anteriores fue el siguiente:

```
<div class="card">
    <img class="card__image" src="/image.png" alt="Crew Dragon" />
    <button class="button button--active"></button>
</div>
```

Donde, el CSS se ve de la siguiente forma:

```
.card {
    ...
}
.card__image {
    ...
}
.button {
    ...
}
.button--active {
    ...
}
```

Pero si usamos SASS, nuestros estilos se verían de la siguiente forma:

```
.card {
    &__image {
        ...
    }
}
.button {
    &--active {
        ...
    }
}
```

Aquí sólo alcanzamos a reducir 2 líneas de código, pero, ¿te alcanzas a imaginar cuántas líneas de código podríamos ahorrarnos en un proyecto con mucho más HTML y CSS? Este es uno de los súper poderes de combinar BEM con SASS, aparte de que se ve mucho más lindo y limpio nuestro código.

## Recomendaciones finales

Los proyectos que usan BEM son fáciles de leer, muy intuitivos y permiten evitar los selectores de CSS anidados. También, es una herramienta que permite personalizar las reglas y nomenclatura para tener un código mucho más limpio y escalable.

> Recursos de imágenes: [https://www.spacex.com](https://www.spacex.com/)

Si quieres aprender todo lo necesario para convertirte en Frontend Developer construyendo un proyecto profesional desde cero, te espero en el [Curso de Frontend Developer](https://platzi.com/frontdev) en Platzi.