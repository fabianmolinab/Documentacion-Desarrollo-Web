
### getByRole()

es un localizador que permite la detección de elementos dentro del DOM como atributos orientados al usuario.

```html
<div id="header">	
	<h1 class="h1-body">Hola Mundo</h1>
</div>
```

```typescript
	page.getByRole("heading",{name="Hola Mundo"})

```

Se podría mejorar con un *locator* para hacerlo mas especifico de la siguiente manera:

```typescript
	page.locator('#header')
		.getByRole("heading", { name="Hola Mundo" })
```

### getByText()

es un localizador por texto dentro de los tags htmls, la sintaxis seria las siguiente `page.getByText("texto", {exact:true})`, se recomienda el  *exact* para que la busqueda se exacta al string del metodo ejemplo:

```html
<p>Este es un buen parrafo</p>
<h1>Este es un buen parrafo y titulo</h1>
```

```typescript
	page.getByText("Este es un buen parrafo").toBeVisible()
```

Si la busqueda se hace como de esa forma va tomar ambas etiquetas como validas pero si le agregamos el exact va tomar justo la etiqueta html que contenga ese texto.

```typescript
	page.getByText("Este es un buen parrafo", {exact:true} )
```

