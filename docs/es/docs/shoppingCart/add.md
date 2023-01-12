# Añadir elementos al carrito

Este método nos permite añadir actividades, alojamientos y/o paquetes al carrito de la compra.

Puede ser llamado una o varias veces, según nuestras necesidades para ir añadiendo elementos al carrito.

Podemos añadir uno o varios elementos en una o varias llamadas, según las necesidades en el proceso de integración.

## Método de acceso

**POST** /ShoppingCart/Add

## Estructura de la petición

- **``ShoppingCartId``**: (``string``) ``Requerido``. Identificador del carrito.
- **``Activities``**: (``list``) ``Opcional``. Listado de actividades a añadir al carrito.
    - **``Activity``**: (``object``) ``Opcional``. Información de la actividad.
        - **``ProductId``**: (``string``) ``Requerido``. Indentificador del producto.
        - **``AccessDateTime``**: (``dateTime``) ``Requerido``. Indentificador del producto.