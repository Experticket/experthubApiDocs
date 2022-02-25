# Interfaz de comunicación

El canal de comunicación será un API REST:

- Llamadas HTTP a una URL.
- Con un HTTP verb (POST, GET, DELETE...).
- Un *request body* o cuerpo.
- Content negotiation: Se puede elegir entre trabajar con XML o con JSON, dependiendo del REQUEST HEADER "Accept" y/o "Content-Type" que se envíe. Para XML se envía "application/xml" y para JSON "application/json". Si ignoramos el REQUEST HEADER, por defecto la respuesta será de tipo JSON. Hay que tener en cuenta que "Content-Type" se utiliza para las peticiones y "Accept" para las respuestas.
- Si se opta por trabajar con XML, se pueden descargar los [XSDs](http://www.123.com).
