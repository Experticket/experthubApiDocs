# Conexión

El canal de comunicación será un API REST:

- Llamadas HTTP (POST, GET, DELETE...) a una URL.
- La información se enviará a través de un *query string* que forme parte de la URL o mediante un *request body* en función del método HTTP que usemos.
- REQUEST HEADERS:
    - "Accept" debe ser "application/json".
    - "Content-Type" debe ser "application/json".
    - "Authorization" debe de contener la palabra *ApiKey* seguida de un espacio y el ApiKey que tengamos (p.ej. `Authorization: ApiKey XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX`).
