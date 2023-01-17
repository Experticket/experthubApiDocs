# Obtención de la documentación

Este método permite obtener la documentación de una venta confirmada.

## Método de acceso

**GET** /ShoppingCart/Documentation

## Estructura de la petición

Requiere pasarle, como parámetro de la url (`query string`), los siguientes parámetros:

- **`ShoppingCartId`**: (``string``).  ``Requerido``Indica si la llamada ha sido procesada satisfactoriamente.

### Ejemplo de llamada

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/documentation.request.1.md"

## Estructura de la respuesta

Devuelve un array de bytes, que conforman el PDF (``Byte[]``).
