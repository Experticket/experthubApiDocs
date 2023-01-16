# Obtención de la documentación

Este método permite obtener la documentación de una venta confirmada.

## Método de acceso

**GET** /ShoppingCart/Documentation

## Estructura de la petición

Requiere pasarle, como parámetro de la url (`query string`), los siguientes parámetros:

- **``ShoppingCartId``**: (``string``) ``Requerido``. Identificador del carrito.


### Ejemplos

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/documentation.request.1.md"

## Estructura de la respuesta

- **`Success`**: (``boolean``). Indica si la llamada ha sido procesada satisfactoriamente.
- **`Documents`**: (``list``). Listado de documentos.
    - **`Document`**: (``object``). Información del documento.
        - **`SalesDocumentUrl`**: (``string``). Url del documento.

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/documentation.response.1.md"