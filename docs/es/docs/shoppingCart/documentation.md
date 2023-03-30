# Obtención de la documentación

Este método permite obtener la documentación de una venta confirmada en los idiomas especificados.

## Método de acceso

**GET** /ShoppingCart/Documentation

## Estructura de la petición

Requiere pasarle, como parámetro de la url (`query string`), los siguientes parámetros:

- **`ShoppingCartId`**: (``string``).  ``Requerido`` Indica si la llamada ha sido procesada satisfactoriamente.
- **`Language`**: (``list``).  ``Opcional`` Indica el idioma en el que se descargará la documentación.
  
!!! warning ""
    Si no se especifica el campo ``Language``, se descargará en el idioma por defecto del colaborador. Si se especifica más de un idioma repitiendo la query tantas veces como idiomas se requieran, se descargará un único PDF con la documentación en tantos idiomas como se haya especificado.

### Ejemplo de llamada

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/documentation.request.1.md"

## Estructura de la respuesta

Devuelve un array de bytes, que conforman el PDF (``Byte[]``).
