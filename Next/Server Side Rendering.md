## Intro

El otro día en el Máster Front End Lemoncoders, [Erik Rasmussen](https://twitter.com/erikras?lang=es) nos dió una sesión muy interesante sobre server side rendering y cómo implementarlo usando React y Next. Eso nos ha animado a escribir una serie de posts en la que explicamos cómo funciona esto de manera detallada.

En este primer artículo de la serie vamos a centrarnos en  es explicar bien el problema que viene a resolver "Server side rendering" así como conceptos de base, en siguientes entrega nos meteremos de lleno en una implementación utilizando Next y React.

## Esto suena a termino de moda, ¿para qué sirve?

Básicamente para cubrir dos áreas oscuras del desarrollo moderno:

-   SEO (Search Engine Optimization): es decir que los buscadores de Google te encuentren e indexen tu contenido.
-   Aumentar la velocidad en la carga inicial de tu sitio: es decir que la primera vez que accedas a tu sitio lo haga más rápido.

_Cooomooor ¿me estás diciendo que una aplicación Angular o React tiene problemas para que Google las posicione? ¿Me estás diciendo que con todo lo moderno que son estos frameworks / librerías pueden tener problemas de rendimiento al servir la primera página?_ Correcto, veamos por qué.

## El problema del SEO

Imaginemos la web de un sitio de reservas de hotel.

A nivel de SEO _¿Cómo funciona un crawler?_  (esto es: los robotitos que van leyendo contenidos de internet para pasarle información a los buscadores).

![crawler.png](https://images.squarespace-cdn.com/content/v1/56cdb491a3360cdd18de5e16/1526313722627-26XN8J7AI4ZM9XMVKOIG/crawler.png?format=1000w)

_¿Qué hace que un Razor / JSP o similar sea SEO friendly?_ Que todas las transformaciones se hagan en servidor y siempre acabemos sirviendo páginas HTML con un JavaScript asociado.

![flujo_crawler_server.png](https://images.squarespace-cdn.com/content/v1/56cdb491a3360cdd18de5e16/1526301209784-3FNT741KHPGS200QITU2/flujo_crawler_server.png?format=1000w)

¿Qué hace una tecnología como React, Angular o Vue? Armar la página una vez que está en el lado cliente, ¿Qué pasa entonces con los crawlers?  Que se hacen un lío y no pueden leer bien el contenido de nuestra página.

![crawler_jsx.png](https://images.squarespace-cdn.com/content/v1/56cdb491a3360cdd18de5e16/1526301306483-IKVUBNMVUNK05UU8XYIW/crawler_jsx.png?format=1000w)

_¿Y por qué es tan importante esto del SEO?_ Si del éxito de tu empresa depende que tu contenido aparezca en Google es algo crítico, ejemplos: una web de reservas de hotel, vuelos, una tienda que vende productos... si lo que haces son aplicaciones de negocio (como puede ser el propio motor de reservas de un hotel, o una aplicación de banca online) no te hará falta, de hecho hasta hace no mucho se solía partir en dos un desarrollo web:

-   La parte de contenido, que la desarrollabas con una tecnología SEO friendly (por ejemplo un CMS) .
-   La parte de "chicha", la que tiene negocio, es decir, todo lo que hay detrás cuando le das clic a comprar, reservar, operar...

Con _server side rendering_ ya no nos hace falta realizar esta separación.

## El problema de la primera carga

_Vaaaleee te compro lo del SEO, pero... ahora ¿cómo me vas a decir que la primera carga en una aplicación moderna puede ser más lenta que con lenguajes de generación de markup en servidor tipo Razor o JSP?_ Veamos el porqué, cuando montamos una página con una tecnología de generación de markup en servidor, todo se genera desde recursos locales (o al menos servidores que tenemos a mano):

![primera_carga_jsp.png](https://images.squarespace-cdn.com/content/v1/56cdb491a3360cdd18de5e16/1526301458604-79SH45EWQIKWU5318F6V/primera_carga_jsp.png?format=1000w)

Cuando tenemos que servir por primera vez una página desde una tecnología moderna (React, Angular, Vue...), tenemos primero que cargar el HTML + JavaScript, y después dar otro salto para pedir los datos que nos hacen falta y ya pintar la página.

![primera_peticion_jsx.png](https://images.squarespace-cdn.com/content/v1/56cdb491a3360cdd18de5e16/1526301568179-4RM5MZOOFLB3CLONXE9F/primera_peticion_jsx.png?format=750w)

Es algo así como si fueras a casa de tus padres y en vez saquearles la nevera de primeras, esperaras a volver a tu piso para pedirles que te envíen _"los tupper"_ por mensajero.

_¿No sería mejor que esos datos ya vinieran precargados?_ Eso es, veo que vas por buena camino... en esto consiste  "server side rendering".

_Ok, lo entiendo pero ¿tan importante es esa diferencia de segundos?_ Aplícatelo a ti mismo, a que más de una vez eres impaciente cuando navegas por internet o incluso en mitad de la carga te arrepientes de comprar algo, una página que tarde más en cargar que la competencia se traduce en una página que vende menos, una página que sea un poco lenta en cargar se traduce en clientes que se arrepienten de haber clickado y se meten a otra cosa es decir... [tu empresa pierde dinero y eso hace daño](https://blog.gigaspaces.com/amazon-found-every-100ms-of-latency-cost-them-1-in-sales/).

## Y.. ¿Por qué las soluciones de generación markup en servidor no son buenas?

Seguro que ahora estarás pensando en: _volvamos al JSP / Razor y dejémonos de modernidades..._  pues esa solución nos no vale tampoco, veamos por qué:

-   Hoy en día las páginas en cliente tienen una funcionalidad muy rica, es decir mucha lógica en JavaScript, el Razor / JSP se basa en hacer una "fritanga" entre código de servidor y código de cliente, a más complejidad que tengan las páginas más complejo son de mantener (campos ocultos, datos que van de ida y vuelta, etc...).
-   Si siempre trabajamos con páginas basadas en Razor / JSP, la primera carga será más rápida, pero las subsecuentes no, tendremos que hacer un viaje a servidor, cargar la siguiente página, servirla... cuando es más fácil tenerlo todo precargado en una SPA y sólo pedir datos.
-   Además si vamos pidiendo páginas nuevas, se pierde el estado en nuestro navegador (o bien enviamos esta información a servidor y tenemos sesión en servidor, o tenemos que utilizar algún mecanismo tipo _session storage_, _cookies_...).
-   Otro problema adicional es que cargamos a nuestro servidor con el coste de tener que generar páginas HTML, ¿No es mejor que haga ese trabajo el navegador del cliente?

_Ahora sí que me habéis liado del todo. ¿Podemos hacer algo que una lo mejor de los dos mundos? ..._

## Server Side Rendering al rescate

¿Y si tuviéramos una tecnología que nos permitiera en la primera petición servir directamente la página ya montada (incluyendo el estado de nuestras variables en JavaScript), y en subsecuentes que tirara siempre del navegador y sólo pidiera datos vía llamadas AJAX? _Eso pinta bien, pero será complejo de narices, ya que yo puedo navegar por primera vez desde la página principal (por ejemplo la página principal de un sitio de reservas hoteleras), o que un amigo me pase una página concreta de ese sitio (por ejemplo la ficha de un hotel concreto), y que sea la primera vez que navegue en mi navegador... además de esto, ¿Tendría que hacer  un código específico en cliente y otro en servidor? ¡Vaya lío! ...._

Aquí es donde entre la magia del _server side rendering:_ ¿y si te digo que adoptando librerías y lenguajes adecuados puedes aprovechar la mayoría del código y apenas tener que hacer algún cambio ligero? ¿A que suena interesante?.

## ¿Cómo consigo que esto pinte en servidor y cliente?

Recuerdo hace unos años cuando era tan feliz programando con C# y .NET en servidor, y con JavaScript en cliente... y en eso alguien me dijo _ahora vais a tener JavaScript en el servidor_, y le conteste _peeero que diiices eso no tiene futuro_... bueno empecemos a ver porque JavaScript es el presente y el futuro (con el permiso de _WebAssembly_ claro): si tu página web se monta en cliente con JavaScript, ¿Qué pasa si tu servidor se basa en el motor de Chrome y el lenguaje que utiliza es JavaScript? ... pues que se convierte en algo viable replicar los mismos pasos que damos en cliente, en el lado del servidor.

![js_server_client.png](https://images.squarespace-cdn.com/content/v1/56cdb491a3360cdd18de5e16/1526301700322-IPYU0TAXS7N0VO6HC1P7/js_server_client.png?format=1000w)

As que eso de tener JavaScript corriendo en el servidor cobra sentido.

## ¿Y las llamadas a API's REST...?

Lo suyo es que tengamos servidores de front end puros (que sirvan páginas, y que trabajen con JavaScript), y servidores que sirvan datos (por ejemplos API's REST o GraphQL, aquí usando el lenguaje en el que estemos más a gusto). En principio podemos hacer un _fetch_ para pedir datos a esas API's tanto desde servidor como de cliente... hasta aquí parece que todo bien, pero nos podemos topar con un problema serio... **LA SEGURIDAD:** cuando estamos autenticados, tenemos cookies y headers que arrastran por ejemplos tokens de sesión, ¿Qué podemos plantear?

**Opción 1:** En el lado servidor no hay problemas en setear las cookies que hagan falta para poder hacer peticiones, en el lado cliente por seguridad el navegador web puede limitar el envío de esas cookies a una API REST que no esté en el mismo dominio (o no queremos liarnos la manta a la cabeza arrastrándolas y configurando servidores). En este caso lo que podemos hacer es que el propio servidor web de front end haga de "palanca", es decir tenga un proxy que a peticiones del mismo dominio (por ejemplo las que tengan como prefijo "/api" en la ruta), las redirija al servidor que toque, y esa respuesta se la envíe al cliente (digamos que es como si engañaramos al navegador).

![proxy_server.png](https://images.squarespace-cdn.com/content/v1/56cdb491a3360cdd18de5e16/1526308731053-A8VMAYCQL4EU1QHF521L/proxy_server.png?format=1000w)

> “Cuando montamos este proxy solemos configurarlo para que este cerca del servidor de API, y por otro lado las librerías de server side rendering suelen traer infraestructura para hacernos más fácil su implementación.”

**Opción 2:**  Si usamos una API moderna podemos tener bien configurado CORS y arrastrar las cookies y demás, en este caso, la solución es mucho más directa, no nos hace falta servidor de proxy, ya que tanto cliente como servidor acceden a un servidor tercero de API's.

![cors.png](https://images.squarespace-cdn.com/content/v1/56cdb491a3360cdd18de5e16/1526308831061-RSWRM9TL04BT2KK3PODU/cors.png?format=1000w)

> “Configurar bien CORS no tiene porque ser una tarea fácil, más cuando estamos trabajando con proyectos legacy o a los que no tenemos acceso, por eso la opción 1 es muy popular.”

## ¿Y qué pasa con las variables que guardan estado?

Ese es un buen desafío, una vez que tu código se ha ejecutado en servidor y el HTML está servido, seguramente te haga tener en tu página de clientes valores de variables que ya estén informados, por ejemplo, imagina que tienes una lista de hoteles y la página en cliente (en React esto sería el estado de la aplicación), aquí lo que se hace es que se alimentan en un script que se ejecuta al inicio de la carga de la página en cliente.

_Uy... esto parece que se puede complicar si tengo mucha información dinámica, ¿es así?_ Sí, para solucionar esto, tenemos una solución simple pero no fácil, si usamos Redux, tenemos todo el estado de la aplicación separado en un _store_, sólo necesitamos serializar ese estado en una variable global (_deshidratarlo_), y tener un script para que cuando se cree el store en la ejecución de la página de cliente lo restaure (_lo rehidrata_).

![rehidratar.png](https://images.squarespace-cdn.com/content/v1/56cdb491a3360cdd18de5e16/1526312212079-DLAN2CUZHL3PMIBKRU6B/rehidratar.png?format=1000w)

> “Lo de deshidratar/rehidratar, podíamos compararlo con los alimentos que viene en sobre y los mezclamos con agua para que tengan un aspecto medio decente, sería algo parecido a serializarlo / deserializarlo.”

## ¿Qué diferencia tiene esto con ASP.NET / Razor / JSP...?

Esto punto es muy importante, y es el que más cuesta de entender:

-   En un sitio que corre con ASP.NET / Razor / JSP / PHP, lo que hacemos es que se fabrica una página en servidor, y al cliente siempre se sirve HTML/JS, el JS puede hacer sus llamadas AJAX y demás, pero cuando pedimos otra página, volvemos a ir a servidor, perdemos todo el estado que teníamos en cliente, y volvemos a servir una página nueva en la que empezamos de nuevo.
    
-   En un sitio que corre con _server side rendering_, la primera vez generamos una página con el HTML/JS necesario, una vez que estamos en cliente, hacemos llamadas AJAX para pedir los datos que hagan falta, y si queremos cargar otra página ya sólo cargamos  datos (el HTML ya lo teníamos precargado o lo pedimos como recursos al ser una aplicación SPA).

Es decir en _server side rendering_, la generación de página en servidor sería algo parecido al tanque de combustible auxiliar que lleva un transbordador espacial, sólo lo usa para la fase de despegue. Una vez que ha pillado altura se desprende de él y nunca más lo usará en ese viaje (para el resto de páginas que se quieran visitar, se encarga la instancia del navegador en renderizarlas). 

## No pillo bien el flujo, ¿cómo va?

Como sumario de lo que hemos visto vamos a resumir el flujo en estos dos diagramas.

1\. Cómo sería la carga de una primera página (el servidor genera y sirve HTML / JS).

![primeracarga.png](https://images.squarespace-cdn.com/content/v1/56cdb491a3360cdd18de5e16/1526312719846-0C9VR9D5IFME4LYLSNV9/primeracarga.png?format=1000w)

2\. Una vez que la primera página esta generada, nunca más volvemos a generar para esa sesión una página en servidor, ya se genera en cliente (y el cliente se encarga de cargar los datos vía llamadas AJAX), dependiendo de la implementación atacaremos un proxy server o directamente el servidor de API.

![siguientes_cargas.png](https://images.squarespace-cdn.com/content/v1/56cdb491a3360cdd18de5e16/1526312745735-R8I6HLM8LZSD2E3DNW4Z/siguientes_cargas.png?format=1000w)

Esto lo podemos comparar con cómo funciona el tanque de un transbordador espacial, sólo lo usamos para el despegue, una vez que estamos bien alto, el tanque se desprende, y tiras con tus propios motores.

## Conclusión

Esto del _server side rendering_ es algo muy potente, permite unir lo mejor de los dos mundos (generación de markup en servidor y en cliente), y lo que es mejor desarrollar con las tecnologías con las que estemos más a gusto sin tener que preocuparnos de posicionamiento web, ni perdida de rendimiento.

En el siguiente post de esta serie, pasamos de la definicíon de conceptos a la práctica, implementado una aplicación con _server side rendering_ utilizando Next y React.

## Agradecimientos

Este post cuenta con un revisor de lujo [Erik Rasmussen](https://twitter.com/erikras), autor de propuestas y proyectos open source tales como: [Redux-Form](https://github.com/erikras/redux-form),  [Ducks Modular Redux](https://github.com/erikras/ducks-modular-redux), [React Final Forms](https://github.com/final-form/react-final-form).

## ¿Con ganas de aprender desarrollo Front End?

Si tienes ganas de ponerte al día en el mundo del Front End impartimos un máster online con clases en vivo, más información: [http://lemoncode.net/master-frontend](http://lemoncode.net/master-frontend)