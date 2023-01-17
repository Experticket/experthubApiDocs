# Eliminar un elemento del carrito

Este método permite eliminar un elemento existe en el carrito. Para ello es necesario utilizar el Identificador (**``Id``**) que se muestra en la respuesta del método [**``Add``**](./add.md#estructura-de-la-respuesta).

## Método de acceso

**POST** /ShoppingCart/Remove

## Estructura de la petición

- **``ShoppingCartId``**: (``string``) ``Requerido``. Identificador del carrito.
- **``ShoppingCartItemIdsToRemove``**: (``list``) ``Requerido``. Listado de identificadores a eliminar.
    - **``(string)``**: ``Requerido``. Identificador a eliminar. Este identificador es mostrado en la respuesta del método [**``Add``**](./add.md#estructura-de-la-respuesta).

### Ejemplos

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/remove.request.1.md"

## Estructura de la respuesta

- **`Success`**: (``boolean``). Indica si la llamada ha sido procesada satisfactoriamente.

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/remove.response.1.md"