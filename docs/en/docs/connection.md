# Communication interface

The communication interface is based on a REST API.

- HTTP calls (`POST`, `GET`, `DELETE`...) to a specific method (*endpoint*).
- Depending on the method used, data may be sent through a *query string* that is part of the URL, or through a *request body* in JSON format.
- The following HTTP headers must be added to all requests:

    | Header name | Header value |
    | --- | --- |
    |`Accept` | `application/json` |
    |`Content-Type` | `application/json` |
    |`Authorization` | `ApiKey YOUR_API_KEY` |
