# LiveView

- ¿Qué es LiveView?
- Para responder a esto, vamos a empezar con un escenario común.
- Digamos que tenemos una aplicación Phoenix, y en esta página hay un botón.
- Al hacer clic en él, se cambia algún estado en el servidor, y se envía una nueva página de HTML, y luego se recarga toda la página, aunque sólo haya cambiado una parte de ella.
- Pero eso está lejos de ser lo ideal.
- Al hacer clic en el botón sólo deberían actualizarse las partes relevantes de la página.
- Eso sería más interactivo.
- Sí. Así que un enfoque que podríamos tomar es lanzar algo de código AJAX.
- Tendríamos que escribir algo de JavaScript en el front-end, ya sea con Vanilla JavaScript, o usando una librería o framework JavaScript del lado del cliente, como React, Vue o Angular.
- Y luego escribiríamos algo de Elixir en el backend.
- Sí, si hiciéramos eso, cuando el botón sea pulsado, nuestro JavaScript enviaría una petición asíncrona de JavaScript, o AJAX, al servidor.
- Tendríamos una ruta y una acción de controlador configurada para tratar la solicitud, y enviar un trozo de JSON de vuelta como respuesta.
- Y entonces nuestro JavaScript actualizaría dinámicamente partes del DOM para reflejar los cambios.
- Otro enfoque es evitar la sobrecarga del ciclo de solicitud-respuesta HTTP dejando que el cliente-servidor hable a través de una conexión WebSocket persistente.
- Para ello, estableceríamos un canal Phoenix, y nuestro JavaScript se uniría a ese canal.
- Entonces, cuando se pulse el botón, nuestro JavaScript empujaría un evento por el WebSocket al proceso del servidor del canal.
- Manejaría ese evento, cambiaría el estado del proceso, y empujaría JSON de vuelta al cliente a través del WebSocket.
- Y al igual que con AJAX, nuestro JavaScript actualizaría dinámicamente el DOM.
- Sí. Ambos enfoques harían que la página se sintiera más interactiva, pero todavía tendríamos que escribir JavaScript del lado del cliente para manejar los eventos del DOM, como los clics de los botones, comunicarse a través del WebSocket, y actualizar el cliente en consecuencia.
- Dependería totalmente de nosotros mantener el cliente sincronizado con el servidor.
- ¿Y si hubiera una forma de prescindir del JavaScript personalizado, mantener la conexión persistente entre el cliente y el servidor, y hacer que el cliente se actualice automáticamente cuando se produzcan cambios en el servidor, o incluso actualizar varios clientes al mismo tiempo?
- Ah. Bueno, eso es lo que nos da LiveView.
- Es una librería que abstrae todos los detalles mundanos, pero importantes, para que podamos centrarnos en añadir características interactivas en tiempo real a nuestra aplicación.
- Ahora, obviamente tiene que haber algo de JavaScript corriendo en el navegador, pero no tenemos que escribirlo.
- Viene a lo largo del viaje con LiveView.
- Cuando hacemos que nuestra página sea un LiveView, y luego se pulsa el botón, ese pequeño trozo de JavaScript empuja automáticamente un evento por el WebSocket a un proceso LiveView.
- Este maneja ese evento.
- El estado del proceso es cambiado, y una nueva view es renderizada. 
- Ahora, mientras que otras tecnologías que realizan el renderizado del lado del servidor a menudo envían toda la página en cada evento del cliente, LiveView sabe exactamente lo que ha cambiado, y sólo envía los cambios relevantes a la página.
- El JavaScript de LiveView fusiona entonces esas actualizaciones en el DOM.
- Así, a medida que el proceso LiveView recibe nuevos eventos del cliente, todo se mantiene automáticamente sincronizado sin tener que escribir ningún JavaScript y es realmente eficiente, tanto en términos de lo que está en el cable, como en la forma en que el DOM es parcheado.
- Ahora, en lugar de escribir JavaScript del lado del cliente, escribimos Elixir del lado del servidor.
- Un LiveView es un módulo con tres funciones de callback.
- Mount asigna el estado inicial del proceso LiveView.
- Handle event cambia el estado del proceso, y render renderiza una nueva view para el nuevo estado actualizado.
- Es un modelo de programación bastante simple que hace que LiveView sea muy divertido de usar.
- Ahora entraremos en todos los detalles, pero por ahora, hay dos cosas más que vale la pena mencionar que hacen que LiveView sea único.
- En primer lugar, dado que las LiveViews son renderizadas por el servidor, la petición original es simplemente una petición HTTP normal.
- Por lo tanto, el cliente recibe una respuesta inicial rápida de HTML estático, lo que tiene la ventaja añadida de hacerla amigable para el SEO sin necesidad de complejidad adicional.
- En segundo lugar, dado que las LiveViews utilizan una conexión WebSocket persistente después de la solicitud inicial, los cambios en el servidor también pueden ser enviados a múltiples clientes.
- Esto es realmente importante para construir aplicaciones distribuidas en tiempo real.
- Conseguimos todo esto sin necesidad de tocar el cliente.
- Me atrevo a decir que LiveView trae el calor sin ninguna de las quemaduras.

En resumen, LiveView ofrece algunas características únicas:

Como las vistas en vivo son renderizadas por el servidor, la petición inicial es sólo una petición HTTP normal. Así, el cliente obtiene una respuesta inicial rápida de HTML estático que tiene la ventaja añadida de hacerla amigable para el SEO sin necesidad de una complejidad extra.

LiveView utiliza una conexión websocket persistente después de la solicitud inicial, de modo que las aplicaciones LiveView reaccionan casi instantáneamente a los eventos del usuario. Los cambios en el servidor también pueden ser enviados a múltiples clientes. Esto es realmente importante para construir aplicaciones distribuidas en tiempo real.

Mientras que otras tecnologías que realizan el renderizado del lado del servidor suelen enviar toda la página en cada evento del usuario, LiveView sabe exactamente lo que ha cambiado y envía a los clientes sólo los valores modificados.

LiveView está construido sobre la plataforma Phoenix, de probada eficacia, por lo que puede manejar de forma fiable millones de conexiones simultáneas de websocket.

Los resultados son espectaculares y cambian el juego:

  * tanto el cliente como el servidor están sincronizados, siempre y sin problemas
  * conexiones persistentes altamente optimizadas para la escala web
  * interfaces de usuario robustas y resistentes, para que pueda seguir funcionando
  * una base de código unificada que es más fácil de mantener
  * sin JavaScript personalizado ni dependencias externas

Ah, sí, y LiveView también tiene un modelo de programación simple (casi adictivo) que hace que sea una biblioteca realmente divertida de usar. Nos gustó tanto, de hecho, que no podíamos dejar de usarla para construir todo tipo de características de interfaz de usuario interactiva que tradicionalmente requieren JavaScript personalizado. Y los resultados nos han sorprendido.