# Creación de un carrito

Este método nos permite crear un carrito de la compra para ir añadiendo productos.

## Método de acceso

**POST** /ShoppingCart/Create

## Estructura de la petición

No hay cuerpo en la petición.

## Estructura de la respuesta

- **``Success``**: (``boolean``). Indica si la solicitud se ha podido satisfacer correctamente.
- **``Id``**: (``string``). Identificador del carrito.

### Ejemplos

??? tip "Ejemplos"
    
    --8<-- "includes/examples/shoppingCart/create.response.1.md"