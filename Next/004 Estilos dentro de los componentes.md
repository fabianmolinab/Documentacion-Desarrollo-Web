# Estilos dentro de los componentes

Dentro de los componentes de en Next se puede introducir estilos con la siguiente etiqueta:

```jsx
<style jsx>{`... Todos lo estilos`} </style>`
```

## ¿Como colocar estilos globales?

- La primera forma se implementa con los estilos dentro de los componentes como en el ejemplo anterios pero añadiendo el atributo **global,** seria la siguiente manera:
	
	`<style jsx global>{``}</style>`
	
- Desde *_app.ts* o *_app.js* podemos importar los estilos globales desde otro archivo con los estilos.  Creamos el archivo *styles/globals.css* y luego lo importamos en *_app.ts.* Esta es la forma recomendada. 


###### Tags: #next #react #estilos 