# Confirmación de la reserva

Este método permite obtener la documentación de una venta confirmada.

## Método de acceso

**GET** /ShoppingCart/Documentation

## Estructura de la petición

Requiere pasarle, como parámetro de la url (`query string`), los siguientes parámetros:

- **``ShoppingCartId``**: (``string``) ``Requerido``. Identificador del carrito.


### Ejemplos

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/documentation.request.1.md"

```
{{url}}/ShoppingCart/Documentation?ShoppingCartId=gghy31ch6g3rs
```

## Estructura de la respuesta

- **`Success`**: (``boolean``). Indica si la llamada ha sido procesada satisfactoriamente.
- **`ExperticketSales`**: (``list``). Listado de ventas asociadas en Experticket.
    - **`ExperticketSale`**: (``object``). Información de la venta.
        - **`Id`**: (``string``). tbd

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/sale.response.1.md"