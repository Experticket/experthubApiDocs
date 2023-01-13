# Eliminar la reserva

Este método permite eliminar la reserva ya creada e invalida el carrito.

## Método de acceso

**POST** /ShoppingCart/CancelConfirm

## Estructura de la petición

- **``ShoppingCartId``**: (``string``) ``Requerido``. Identificador del carrito.

### Ejemplos

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/cancelConfirm.request.1.md"

## Estructura de la respuesta

- **`Success`**: (``boolean``). Indica si la llamada ha sido procesada satisfactoriamente.

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/cancelConfirm.response.1.md"