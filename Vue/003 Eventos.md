# Eventos

Los eventos son acciones o interacciones que ocurren en la interfaz de usuario, como hacer click, enviar formulario, mover mouse, pulsar teclas, etc. 

Para manejar los eventos en Vue, utilizando [directivas](./002 Directivas.md) en especifico la `v-on`, la cual se encarga de ejecutar metodos o expresiones de respuesta.

## Directiva v-on

Como anteriormente dicho esta directiva es la encargada de gestionar los eventos dentro del DOM, haciendo más comodo y practico su utilización, ya que en javascript se usa la función `.addEventListener()`. Si quieres saber mas del tema [eventos nativos en webcomponents](https://lenguajejs.com/webcomponents/funcionalidad/eventos-en-webcomponents/)

### ¿Cómo rayos funciona v-on?

Para este caso miremos este ejemplo:

```html
<!-- Ejecuta el método incrementarContador cuando se haga clic -->
<button v-on:click="incrementarContador">Incrementar Contador</button>
```

```javascript
export default {
  data() {
    return {
      contador: 0
    };
  },
  methods: {
    incrementarContador() {
      this.contador++;
    }
  }
};
```
Observamos que la directiva `v-on:click` cuando el usuario de click sobre la button ejecutará el metodo *incrementarContador().* 

## Modificadores de eventos

Los modificadores de eventos de la directiva v-on se hace como el mismo nombre lo dice para modificar su comportamiento, se pueden usar los siguientes:

- **.stop:** Llama al método event.stopPropagation() para parar la propagación del evento.
- **.prevent:** Llama al método event.preventDefault() para evitar el comportamiento por defecto.
- **.capture:** Utiliza el modo capture del .addEventListener().
- **.self:** Sólo se dispara si el evento es generado desde el propio elemento.
- **.once:** Sólo se dispara la primera vez. Equivalente al parámetro { once: true }.
- **.passive:** Realiza una escucha pasiva. Equivalente al parámetro { passive: true }.

Con este ejemplo veremos como se aplican los modificadores:

```html
<template>
  <div>
    <button v-on:click.once="showMessage">Avisarme (solo una vez)</button>
    <!-- Equivalente al anterior (y preferido): -->
    <button @click.once="showMessage">Avisarme (solo una vez)</button>
  </div>
</template>
```

### Modificadores de teclas

Para modificadores de teclas tiene un evento especifico por lo general es `@keyup`en la documentación oficial de Vue encontraremos mas especifico los modificadores según el tipo de letra, [Documentación oficial](https://vuejs.org/guide/essentials/event-handling.html#key-modifiers) dentro de las teclas modificadores tienen un tipo especifico:

- .enter
- .tab
- .delete (captures both "Delete" and "Backspace" keys)
- .esc
- .space
- .up
- .down
- .left
- .right

En siguiente ejemplo veremos como funciona:

```html
<template>
  <div>
    <input type="text" v-on:keyup.enter="enviarFormulario">
    <button @click="enviarFormulario">Enviar</button>
  </div>
</template>

<script>
export default {
  methods: {
    enviarFormulario() {
      alert('Formulario enviado');
    }
  }
};
</script>
```

Hemos agregado el modificador de tecla `.keyCode` con el valor `enter` al escuchar el evento `keyup` en el campo de texto. Esto significa que el método `enviarFormulario` solo se ejecutará cuando el usuario presione la tecla "Enter".

El botón "Enviar" también está vinculado al mismo método `enviarFormulario`, lo que significa que el usuario también puede hacer clic en el botón para enviar el formulario.

