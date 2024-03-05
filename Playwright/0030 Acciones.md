## ¡Abracadabra, Acciones Asombrosas! ✨

### Introducción
Playwright tiene el poder de interactuar con los elementos HTML, desde simples clics hasta cargar archivos y ¡mucho más!

### Entrada de Texto
Rellenar formularios es tan fácil como decir "fill". ¡Mira cómo hacemos magia!

```javascript
await page.getByRole('textbox').fill('Peter'); // ¡Texto!
await page.getByLabel('Fecha de Nacimiento').fill('2020-02-02'); // ¡Fecha!
await page.getByLabel('Hora de la Cita').fill('13:15'); // ¡Hora!
await page.getByLabel('Hora Local').fill('2020-03-02T05:15'); // ¡Fecha y Hora!
```

### Casillas y Botones de Radio
Marcar y desmarcar casillas es pan comido con `"setChecked"`. ¡Haz que los elementos bailen al son de tu varita!

```javascript
await page.getByLabel('Acepto los términos').check(); // ¡Check!
expect(page.getByLabel('Suscribirse al boletín')).toBeChecked(); // ¡Chequeo!
await page.getByLabel('XL').check(); // ¡Radio!
```

### Opciones de Selección
Seleccionar opciones en un elemento `<select>` es tan sencillo como lanzar un hechizo. ¡Vamos allá!

```javascript
await page.getByLabel('Elige un color').selectOption('azul'); // ¡Una opción!
await page.getByLabel('Elige un color').selectOption({ label: 'Azul' }); // ¡Por etiqueta!
await page.getByLabel('Elige múltiples colores').selectOption(['rojo', 'verde', 'azul']); // ¡Varias opciones!
```

### Clic del Ratón
Haz clic como un humano común y corriente, ¡o realiza clics especiales con un toque de magia!

```javascript
await page.getByRole('botón').click(); // ¡Clic!
await page.getByText('Elemento').dblclick(); // ¡Doble Clic!
await page.getByText('Elemento').click({ button: 'derecho' }); // ¡Clic derecho!
await page.getByText('Elemento').hover(); // ¡Desplazarse sobre el elemento!
```

### ¡Bajo el Capó!
Estas acciones no son solo trucos de magia, ¡tienen poderes increíbles! Esperan, comprueban, se desplazan y mucho más.

### Forzar el Clic
Cuando las cosas se ponen complicadas, ¡forzar el clic es como un hechizo potente!

```javascript
await page.getByRole('botón').click({ force: true }); // ¡Fuerza bruta!
```

### Clic Programático
Simula clics como si fueran eventos reales, ¡sin magia negra!

```javascript
await page.getByRole('botón').dispatchEvent('clic'); // ¡Evento mágico!
```

### ¡Cuidado, Teclea con Cautela!
Normalmente, usar `locator.fill()` es suficiente, ¡pero si necesitas teclear, hazlo con estilo!

```javascript
await page.locator('#área').pressSequentially('¡Hola Mundo!'); // ¡Paso a paso!
```

### Teclas y Atajos
¿Quieres presionar Enter o dominar el Control+Right? ¡Aquí tienes tu varita!

```javascript
await page.getByText('Enviar').press('Enter'); // ¡Enter!
await page.getByRole('textbox').press('Control+ArrowRight'); // ¡Control+Right!
await page.getByRole('textbox').press('$'); // ¡Dinero en el teclado!
```

### Subir Archivos
Selecciona y carga archivos como un mago del desarrollo.

```javascript
await page.getByLabel('Subir archivo').setInputFiles(path.join(__dirname, 'miarchivo.pdf')); // ¡Un archivo!
await page.getByLabel('Subir archivos').setInputFiles([
  path.join(__dirname, 'archivo1.txt'),
  path.join(__dirname, 'archivo2.txt'),
]); // ¡Varios archivos!
```

### ¡Enfócate, Concentra tu Energía!
Para las páginas dinámicas, utiliza `locator.focus()` para dirigir tu energía hacia el elemento deseado.

```javascript
await page.getByLabel('Contraseña').focus(); // ¡Concéntrate!
```

### ¡Arrastra y Suelta!
Haz el increíble truco de arrastrar y soltar con `locator.dragTo()`. ¡Desliza elementos como por arte de magia!

```javascript
await page.locator('#elemento-a-arrastar').dragTo(page.locator('#elemento-para-soltar')); // ¡Arrastra y suelta!
```

### ¡Arrastrar a Mano!
Si buscas un control preciso, utiliza métodos de bajo nivel como `locator.hover()`, `mouse.down()`, `mouse.move()` y `mouse.up()`.

```javascript
await page.locator('#elemento-a-arrastar').hover(); // ¡Desplázate!
await page.mouse.down(); // ¡Presiona!
await page.locator('#elemento-para-soltar').hover(); // ¡Desplázate nuevamente!
await page.mouse.up(); // ¡Suelta!
```

¡Y ahí lo tienes! Con estas increíbles acciones, estás listo para conquistar el reino de las pruebas automatizadas. ¡Que la magia de Playwright te acompañe siempre! 🎩✨
