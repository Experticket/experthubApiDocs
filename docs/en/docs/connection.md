# Connection

The communication channel will be a REST API:

- HTTP calls (POST, GET, DELETE...) to an URL.
- The information will be sent through a *query string* that is part of the URL or through a *request body* depending on the HTTP method we use.
- REQUEST HEADERS:
    - "Accept" must be "application/json".
    - "Content-Type" must be "application/json".
    - "Authorization" must contain the word *ApiKey* followed by a space and the ApiKey that we have (e.g. `Authorization: ApiKey XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX`).
