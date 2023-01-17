# Eliminar la reserva

Este método permite eliminar la reserva ya creada e invalida el carrito.

## Método de acceso

**POST** /ShoppingCart/CancelConfirm

## Estructura de la petición

- **``ShoppingCartId``**: (``string``) ``Requerido``. Identificador del carrito.

### Ejemplo de llamada

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/cancelConfirm.request.1.md"

## Estructura de la respuesta

--8<-- "includes/experthubResponseBaseDocumentation.es.md"

### Ejemplo de respuesta

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/cancelConfirm.response.1.md"
