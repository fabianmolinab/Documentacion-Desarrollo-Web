# Componentes en Vue.js

Los componentes en Vue.js son bloques de construcción fundamentales que nos permiten construir interfaces de usuario modulares y reutilizables. Cada componente encapsula tanto la estructura HTML, los estilos CSS y la lógica JavaScript asociada, lo que facilita la creación de aplicaciones Vue.js escalables y mantenibles.

## 1. Creación de Componentes

Los componentes en Vue.js se pueden crear utilizando la función `Vue.component()` o mediante la definición de objetos de componente en un archivo `.vue`. Aquí hay un ejemplo de cómo crear un componente simple:

```html
<!-- EjemploComponente.vue -->
<template>
  <div>
    <h1>{{ titulo }}</h1>
    <p>{{ mensaje }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      titulo: 'Ejemplo de Componente',
      mensaje: 'Este es un componente Vue.js'
    };
  }
};
</script>

<style scoped>
/* Estilos específicos del componente */
h1 {
  color: blue;
}
p {
  font-style: italic;
}
</style>
```

## 2. Uso de componentes

Una vez que hemos creado un componente, podemos utilizarlo en cualquier lugar de nuestra aplicación. Para usar un componente, simplemente lo incluimos en el código HTML de otro componente o archivo HTML principal:


```html
<template>
  <div>
    <ejemplo-componente></ejemplo-componente>
    <!-- <ejemplo-componente/> -->
  </div>
</template>

<script>
import EjemploComponente from './EjemploComponente.vue';

export default {
  components: {
    EjemploComponente
  }
};
</script>
```

## 3. Propiedades(Props)
Los componentes pueden aceptar datos dinámicos llamados props (propiedades), que se pueden pasar desde el componente padre. Esto nos permite hacer que nuestros componentes sean más flexibles y reutilizables. Aquí hay un ejemplo de cómo usar props en un componente:

```html
<!-- HijoComponente.vue -->
<template>
  <div>
    <h2>{{ titulo }}</h2>
  </div>
</template>

<script>
export default {
  props: {
    titulo: String
  }
};
</script>
```

```html
<!-- PadreComponente.vue -->
<template>
  <div>
    <hijo-componente titulo="Título del Componente Hijo"></hijo-componente>
  </div>
</template>

<script>
import HijoComponente from './HijoComponente.vue';

export default {
  components: {
    HijoComponente
  }
};
</script>
```

## 4. [Options API Vue](https://lenguajejs.com/vuejs/componentes/options-api/)

### Ejemplo de Uso de la Options API

La conocida como «**Options API**» es la forma tradicional de trabajar con **Vue**, estando disponible tanto en la versión **Vue 2** como en **Vue 3**. Esta modalidad de API se basa en el uso de un objeto que contiene varias propiedades clave para el funcionamiento de los componentes Vue, como por ejemplo las propiedades `props`, `data`, `computed`, `methods`, etc...

```html
<template>
  <div>
    <h1>{{ mensaje }}</h1>
    <button @click="incrementar">{{ contador }}</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mensaje: 'Contador de clics:',
      contador: 0
    };
  },
  methods: {
    incrementar() {
      this.contador++;
    }
  }
};
</script>
```
