# Creación de un carrito

Este método nos permite crear un carrito de la compra (en adelante **carrito**).

El carrito es un contenedor de productos (actividades, alojamientos y/o paquetes). Puede contener 0 o ℕ productos.

Este carrito no expira. No obstante, los productos añadidos sí.

## Método de acceso

**POST** /ShoppingCart/Create

## Estructura de la petición

No hay cuerpo en la petición.

## Estructura de la respuesta

- **``Id``**: (``string``). Identificador del carrito.

--8<-- "includes/experthubResponseBaseDocumentation.es.md"

### Ejemplo de respuesta

??? tip "Ejemplos"

    --8<-- "includes/examples/shoppingCart/create.response.1.md"
