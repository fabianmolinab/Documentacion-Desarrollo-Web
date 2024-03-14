# Selectores y Locators


## Guía Rápida

¡Aquí tienes los localizadores integrados recomendados!

- `page.getByRole()`: para localizar por atributos de accesibilidad explícitos e implícitos.
- `page.getByText()`: para localizar por contenido textual.
- `page.getByLabel()`: para localizar un control de formulario por el texto de la etiqueta asociada.
- `page.getByPlaceholder()`: para localizar un campo de entrada por el marcador de posición.
- `page.getByAltText()`: para localizar un elemento, usualmente una imagen, por su texto alternativo.
- `page.getByTitle()`: para localizar un elemento por su atributo de título.
- `page.getByTestId()`: para localizar un elemento basado en su atributo data-testid (otros atributos se pueden configurar).

```javascript
await page.getByLabel('Nombre de Usuario').fill('Juan');

await page.getByLabel('Contraseña').fill('contraseña-secreta');

await page.getByRole('button', { name: 'Iniciar sesión' }).click();

await expect(page.getByText('¡Bienvenido, Juan!')).toBeVisible();
```

## Localización de Elementos

Playwright viene con varios localizadores integrados. Para hacer las pruebas más sólidas, recomendamos priorizar los atributos visibles para el usuario y los contratos explícitos como `page.getByRole()`.

Por ejemplo, considera la siguiente estructura del DOM.

```html
<button>Iniciar sesión</button>
```

Localiza el elemento por su rol de botón con el nombre "Iniciar sesión".

```javascript
await page.getByRole('button', { name: 'Iniciar sesión' }).click();
```

## Nota

Utiliza el generador de código para generar un localizador y luego edítalo según tus preferencias.

Cada vez que se utiliza un localizador para una acción, se localiza un elemento DOM actualizado en la página. En el fragmento a continuación, el elemento DOM subyacente se localizará dos veces, una vez antes de cada acción. Esto significa que si el DOM cambia entre las llamadas debido a un nuevo renderizado, se utilizará el nuevo elemento correspondiente al localizador.

```javascript
const localizador = page.getByRole('button', { name: 'Iniciar sesión' });

await localizador.hover();
await localizador.click();
```

Ten en cuenta que todos los métodos que crean un localizador, como `page.getByLabel()`, también están disponibles en las clases `Locator` y `FrameLocator`, por lo que puedes encadenarlos y refinar iterativamente tu localizador.

```javascript
const localizador = page
    .frameLocator('#mi-frame')
    .getByRole('button', { name: 'Iniciar sesión' });

await localizador.click();
```

## Localización por Rol

El localizador `page.getByRole()` refleja cómo los usuarios y la tecnología de asistencia perciben la página, por ejemplo, si algún elemento es un botón o una casilla de verificación. Al localizar por rol, generalmente debes pasar el nombre accesible también, para que el localizador señale exactamente el elemento.

Por ejemplo, considera la siguiente estructura del DOM.

```html
Registrarse
 Suscribirse


<h3>Registrarse</h3>
<label>
  <input type="checkbox" /> Suscribirse
</label>
<br/>
<button>Enviar</button>
```

Puedes localizar cada elemento por su rol implícito:

```javascript
await expect(page.getByRole('heading', { name: 'Registrarse' })).toBeVisible();

await page.getByRole('checkbox', { name: 'Suscribirse' }).check();

await page.getByRole('button', { name: /enviar/i }).click();
```

Los localizadores de rol incluyen botones, casillas de verificación, encabezados, enlaces, listas, tablas y muchos más, y siguen las especificaciones de W3C para el rol ARIA, los atributos ARIA y el nombre accesible. Ten en cuenta que muchos elementos HTML como `<button>` tienen un rol definido implícitamente que es reconocido por el localizador de rol.

Ten en cuenta que los localizadores de rol no reemplazan las auditorías de accesibilidad y las pruebas de conformidad, sino que brindan comentarios tempranos sobre las directrices de ARIA.

## Cuándo Usar los Localizadores de Rol

Recomendamos priorizar los localizadores de rol para localizar elementos, ya que es la forma más cercana a cómo los usuarios y la tecnología de asistencia perciben la página.

## Localización por Etiqueta

La mayoría de los controles de formulario suelen tener etiquetas dedicadas que podrían usarse convenientemente para interactuar con el formulario. En este caso, puedes localizar el control por su etiqueta asociada utilizando `page.getByLabel()`.

Por ejemplo, considera la siguiente estructura del DOM.

```html
Contraseña
<label>Contraseña <input type="password" /></label>
```

Puedes completar el campo de entrada después de localizarlo por el texto de la etiqueta:

```javascript
await page.getByLabel('Contraseña').fill('secreta');
```

## Cuándo Usar los Localizadores por Etiqueta

Usa este localizador al localizar campos de formulario.

## Localización por Marcador de Posición

Los campos de entrada pueden tener un atributo de marcador de posición para sugerir al usuario qué valor debe ingresar. Puedes localizar dicha entrada usando `page.getByPlaceholder()`.

Por ejemplo, considera la siguiente estructura del DOM.

```html
nombre@ejemplo.com
<input type="email" placeholder="nombre@ejemplo.com" />
```

Puedes completar la entrada después de localizarla por el texto de marcador de posición:

```javascript
await page
    .getByPlaceholder('nombre@ejemplo.com')
    .fill('playwright@microsoft.com');
```

## Cuándo Usar los Localizadores por Marcador de Posición

Usa este localizador al localizar elementos de formulario que no tienen etiquetas pero sí tienen textos de marcador de posición.

## Localización por Texto

Encuentra un elemento por el texto que contiene. Puedes hacer coincidir por una subcadena, una cadena exacta o una expresión regular cuando uses `page.getByText()`.

Por ejemplo, considera la siguiente estructura del DOM.

```html
¡Bienvenido, Juan!
<span>¡Bienvenido, Juan</span>
```

Puedes localizar el elemento por el texto que contiene:

```javascript
await expect(page.getByText('¡Bienvenido, Juan')).toBeVisible();
```

Establece una coincidencia exacta:

```javascript
await expect(page.getByText('¡Bienvenido, Juan', { exact: true })).toBeVisible();
```

Haz coincidir con una expresión regular:

```javascript
await expect(page.getByText(/¡bienvenido, [A-Za-z]+$/i)).toBeVisible();
```

## Nota

La coincidencia por texto siempre normaliza el espacio en blanco, incluso con coincidencia exacta. Por ejemplo, convierte múltiples espacios en uno, convierte saltos de línea en espacios e ignora el espacio en blanco inicial y final.

## Cuándo Usar los Localizadores por Texto

Recomendamos usar localizadores de texto para encontrar elementos no interactivos como div, span, p, etc. Para elementos interactivos como botón, a, entrada, etc., usa localizadores de rol.

También puedes filtrar por texto, lo cual puede ser útil al intentar encontrar un elemento particular en una lista.

## Localización por Texto Alternativo

Todas las imágenes deben tener un atributo alt que describa la imagen. Puedes localizar una imagen basada en el texto alternativo usando `page.getByAltText()`.

Por ejemplo, considera la siguiente estructura del DOM.

```html
logotipo de playwright
<img alt="logotipo de playwright" src="/img/playwright-logo.svg" width="100" />
```

Puedes hacer clic en la imagen después de localizarla por el texto alternativo:

```javascript
await page.getByAltText('logotipo de playwright').click();
```

## Cuándo Usar los Localizadores por Texto Alternativo

Usa este localizador cuando tu elemento admita texto alternativo, como los elementos img y area.

## Localización por Título

Localiza un elemento con un atributo de título coincidente usando `page.getByTitle()`.

Por ejemplo, considera la siguiente estructura del DOM.

```html
25 problemas
<span title='Conteo de Problemas'>25 problemas</span>
```

Puedes verificar el recuento de problemas después de localizarlo por el texto del título:

```javascript
await expect(page.getByTitle('Conteo de Problemas')).toHaveText('25 problemas');
```

## Cuándo Usar los Localizadores por Título

Usa este localizador cuando tu elemento tenga el atributo de título.

## Localización por ID de Prueba

Probar por IDs de prueba es la forma más resistente de realizar pruebas, ya que incluso si cambia el texto o el rol del atributo, la prueba seguirá pasando. Los QA y los desarrolladores deben definir IDs de prueba explícitos y consultarlos con `page.getByTestId()`. Sin embargo, probar por IDs de prueba no es visible para el usuario. Si el rol o el valor del texto son importantes para ti, considera usar localizadores visibles para el usuario como localizadores de rol y texto.

Por ejemplo, considera la siguiente estructura del DOM.

```html
<button data-testid="direcciones">Itinerario</button>
```

Puedes localizar el elemento por su ID de prueba:

```javascript
await page.getByTestId('direcciones').click();
```

## Cuándo Usar los Localizadores por ID de Prueba

También puedes usar IDs de prueba cuando elijas utilizar la metodología de ID de prueba o cuando no puedas localizar por rol o texto.

## Establecer un Atributo de ID de Prueba Personalizado

Por defecto, `page.getByTestId()` localizará elementos basados en el atributo data-testid, pero puedes configurarlo en tu configuración de prueba o llamando a `selectors.setTestIdAttribute()`.

Establece el ID de prueba para usar un atributo de datos personalizado para tus pruebas.

```typescript
// playwright.config.ts
import { defineConfig } from '@playwright/test';

export default defineConfig({
  use: {
    testIdAttribute: 'data-pw'
  }
});
```

En tu HTML ahora puedes usar data-pw como tu ID de prueba en lugar del data-testid predeterminado.

```html
<button data-pw="direcciones">Itinerario</button>
```

Y luego localiza el elemento como lo harías normalmente:

```javascript
await page.getByTestId('direcciones').click();
```

## Localización por CSS o XPath

Si absolutamente necesitas usar localizadores CSS o XPath, puedes usar `page.locator()` para crear un localizador que tome un selector que describa cómo encontrar un elemento en la página. Playwright admite selectores CSS y XPath, y los detecta automáticamente si omites el prefijo css= o xpath=.

```javascript
await page.locator('css=button').click();
await page.locator('xpath=//button').click();

await page.locator('button').click();
await page.locator('//button').click();
```

Los selectores XPath y CSS pueden estar ligados a la estructura del DOM o la implementación. Estos selectores pueden romperse cuando cambia la estructura del DOM. Las largas cadenas de CSS o XPath a continuación son un ejemplo de una mala práctica que conduce a pruebas inestables:

```javascript
await page.locator(
    '#tsf > div:nth-child(2) > div.A8SBwf > div.RNNXgb > div > div.a4bIc > input'
).click();

await page
    .locator('//*[@id="tsf"]/div[2]/div[1]/div[1]/div/div[2]/input')
    .click();
```

## Cuándo Usar Esto

CSS y XPath no se recomiendan ya que el DOM a menudo puede cambiar, lo que lleva a pruebas no resistentes. En su lugar, intenta encontrar un localizador que esté cerca de cómo el usuario percibe la página, como localizadores de rol, o define un contrato de prueba explícito usando IDs de prueba.

## Localización en Shadow DOM

Todos los localizadores en Playwright, por defecto, funcionan con elementos en Shadow DOM. Las excepciones son:

- Localizar por XPath no penetra en raíces de sombra.
- No se admiten raíces de sombra en modo cerrado.

Considera el siguiente ejemplo con un componente web personalizado:

```html
<x-detalles role=button aria-expanded=true aria-controls=detalles-internos>
  <div>Título</div>
  #shadow-root
    <div id=detalles-internos>Detalles</div>
</x-detalles>
```

Puedes localizar de la misma manera como si la raíz de sombra no estuviera presente en absoluto.

Para hacer clic en `<div>Detalles</div>`:

```javascript
await page.getByText('Detalles').click();
```

Para hacer clic en `<x-detalles>`:

```javascript
await page.locator('x-detalles', { hasText: 'Detalles' }).click();
```

Para asegurarte de que `<x-detal

les>` contenga el texto "Detalles":

```javascript
await expect(page.locator('x-detalles')).toContainText('Detalles');
```

## Filtrado de Localizadores

Considera la siguiente estructura del DOM donde queremos hacer clic en el botón de compra de la segunda tarjeta de producto. Tenemos algunas opciones para filtrar los localizadores para obtener el correcto.

Producto 1
Producto 2
```html
<ul>
  <li>
    <h3>Producto 1</h3>
    <button>Agregar al carrito</button>
  </li>
  <li>
    <h3>Producto 2</h3>
    <button>Agregar al carrito</button>
  </li>
</ul>
```

### Filtrar por Texto

Los localizadores se pueden filtrar por texto con el método `locator.filter()`. Buscará una cadena de texto en algún lugar dentro del elemento, posiblemente en un elemento descendiente, sin distinguir mayúsculas de minúsculas. También puedes pasar una expresión regular.

```javascript
await page
    .getByRole('listitem')
    .filter({ hasText: 'Producto 2' })
    .getByRole('button', { name: 'Agregar al carrito' })
    .click();
```

Usa una expresión regular:

```javascript
await page
    .getByRole('listitem')
    .filter({ hasText: /Producto 2/ })
    .getByRole('button', { name: 'Agregar al carrito' })
    .click();
```

### Filtrar por no tener Texto

Alternativamente, filtra por no tener texto:

```javascript
// 5 artículos en stock
await expect(page.getByRole('listitem').filter({ hasNotText: 'Sin stock' })).toHaveCount(5);
```

### Filtrar por hijo/descendiente

Los localizadores admiten una opción para seleccionar solo elementos que tengan o no tengan un descendiente que coincida con otro localizador. Por lo tanto, puedes filtrar por cualquier otro localizador como `locator.getByRole()`, `locator.getByTestId()`, `locator.getByText()`, etc.

Producto 1
Producto 2
```html
<ul>
  <li>
    <h3>Producto 1</h3>
    <button>Agregar al carrito</button>
  </li>
  <li>
    <h3>Producto 2</h3>
    <button>Agregar al carrito</button>
  </li>
</ul>
```

```javascript
await page
    .getByRole('listitem')
    .filter({ has: page.getByRole('heading', { name: 'Producto 2' }) })
    .getByRole('button', { name: 'Agregar al carrito' })
    .click();
```

También podemos afirmar la tarjeta de producto para asegurarnos de que solo haya una:

```javascript
await expect(page
    .getByRole('listitem')
    .filter({ has: page.getByRole('heading', { name: 'Producto 2' }) }))
    .toHaveCount(1);
```

El localizador de filtrado debe ser relativo al localizador original y se consulta comenzando con la coincidencia del localizador original, no desde la raíz del documento. Por lo tanto, lo siguiente no funcionará, porque el localizador de filtrado comienza a coincidir desde el elemento de lista `<ul>` que está fuera del elemento de lista `<li>` coincidente con el localizador original:

```javascript
// ✖ INCORRECTO
await expect(page
    .getByRole('listitem')
    .filter({ has: page.getByRole('list').getByText('Producto 2') }))
    .toHaveCount(1);
```

### Filtrar por no tener hijo/descendiente

También podemos filtrar por no tener un elemento coincidente adentro.

```javascript
await expect(page
    .getByRole('listitem')
    .filter({ hasNot: page.getByText('Producto 2') }))
    .toHaveCount(1);
```

Ten en cuenta que el localizador interno coincide a partir del externo, no desde la raíz del documento.

## Operadores de Localizadores

### Coincidencia Dentro de un Localizador

Puedes encadenar métodos que crean un localizador, como `page.getByText()` o `locator.getByRole()`, para estrechar la búsqueda a una parte particular de la página.

En este ejemplo, primero creamos un localizador llamado producto al localizar su papel de listitem. Luego filtramos por texto. Podemos usar el localizador del producto nuevamente para obtener el rol de botón y hacer clic en él, y luego usar una aserción para asegurarnos de que solo haya un producto con el texto "Producto 2".

```javascript
const producto = page.getByRole('listitem').filter({ hasText: 'Producto 2' });

await producto.getByRole('button', { name: 'Agregar al carrito' }).click();

await expect(producto).toHaveCount(1);
```

También puedes encadenar dos localizadores, por ejemplo, para encontrar un botón "Guardar" dentro de un diálogo particular:

```javascript
const botonGuardar = page.getByRole('button', { name: 'Guardar' });
// ...
const dialogo = page.getByTestId('dialogo-configuracion');
await dialogo.locator(botonGuardar).click();
```

### Coincidencia de Dos Localizadores Simultáneamente

El método `locator.and()` reduce un localizador existente al hacer coincidir un localizador adicional. Por ejemplo, puedes combinar `page.getByRole()` y `page.getByTitle()` para hacer coincidir por rol y título.

```javascript
const boton = page.getByRole('button').and(page.getByTitle('Suscribir'));

```

### Coincidencia de uno de los dos localizadores alternativos

Si deseas apuntar a uno de los dos o más elementos, y no sabes cuál será, usa `locator.or()` para crear un localizador que coincida con todas las alternativas.

Por ejemplo, considera un escenario donde te gustaría hacer clic en un botón "Nuevo correo electrónico", pero a veces aparece un diálogo de configuración de seguridad en su lugar. En este caso, puedes esperar tanto un botón "Nuevo correo electrónico" como un diálogo y actuar en consecuencia.

```javascript
const nuevoEmail = page.getByRole('button', { name: 'Nuevo' });
const dialogo = page.getByText('Confirmar configuración de seguridad');
await expect(nuevoEmail.or(dialogo).first()).toBeVisible();
if (await dialogo.isVisible())
  await page.getByRole('button', { name: 'Descartar' }).click();
await nuevoEmail.click();
```

### Coincidencia Solo de Elementos Visibles

NOTA: Es mejor encontrar una forma más confiable de identificar de manera única el elemento en lugar de verificar la visibilidad.



Puedes usar el método `locator.isVisible()` para filtrar solo elementos visibles en la página. Por ejemplo, para hacer clic en un botón visible:

```javascript
await page.getByRole('button').isVisible().click();
```

## Iteración de Elementos Localizados

### Obtener todos los Elementos Coincidentes

Puedes usar `locator.all()` para obtener una lista de todos los elementos que coinciden con el localizador. Esto es útil cuando esperas encontrar múltiples elementos y necesitas interactuar con cada uno de ellos.

Por ejemplo, para obtener todos los botones en una lista y hacer clic en cada uno:

```javascript
const botones = page.getAllByRole('button');
for (const boton of botones) {
    await boton.click();
}
```

### Obtener el Primer o Último Elemento Coincidente

Puedes usar `locator.first()` o `locator.last()` para obtener el primer o el último elemento que coincida con el localizador.

Por ejemplo, para hacer clic en el primer botón en una lista:

```javascript
await page.getByRole('button').first().click();
```

## Depuración de Localizadores

### Salida de Depuración de Localizadores

Para depurar un localizador y entender cómo se resuelve, puedes activar la salida de depuración. Esto imprimirá mensajes detallados en la consola sobre cómo se resuelve el localizador.

```javascript
const localizador = page.getByRole('button');
console.log(localizador.toString());
```

### Depurar el Tiempo de Espera del Localizador

Para depurar problemas de tiempo de espera con un localizador, puedes habilitar la salida de depuración para tiempo de espera.

```javascript
const localizador = page.getByRole('button');
await localizador.waitFor();
```
