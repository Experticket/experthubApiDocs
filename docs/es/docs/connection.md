# Interfaz de comunicación

La interfaz de comunicación se basa en una API Rest.

- Llamadas HTTP (``POST``, ``GET``, ``DELETE``...) a un método específico (*endpoint*).
- Dependiendo del método a utilizar, los datos pueden enviarse mediante *query string*, que forme parte de la URL, o mediante un *request body*, en formato JSON.
- Será necesario añadir las siguientes cabeceras HTTP en todas las peticiones:

    | Nombre de la cabecera | Valor de la cabecera |
    | --- | --- |
    |``Accept`` | ``application/json`` |
    |``Content-Type`` | ``application/json`` |
    |``Authorization`` | ``ApiKey YOUR_API_KEY`` |
