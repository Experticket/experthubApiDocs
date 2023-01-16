# Añadir elementos al carrito

Este método nos permite añadir actividades, alojamientos y/o paquetes al carrito de la compra.

Puede ser llamado una o varias veces, según nuestras necesidades para ir añadiendo elementos al carrito.

Podemos añadir uno o varios productos en una o varias llamadas, según las necesidades en el proceso de integración.

## Método de acceso

**POST** /ShoppingCart/Add

## Estructura de la petición

- **``ShoppingCartId``**: (``string``) ``Requerido``. Identificador del carrito.
- **``Activities``**: (``list``) ``Opcional``. Listado de actividades a añadir al carrito.
    - **``Activity``**: (``object``) ``Opcional``. Información de la actividad.
        - **``ProductId``**: (``string``) ``Requerido``. Identificador del producto.
        - **``AccessDateTime``**: (``date``) ``Requerido``. Fecha de acceso. Formato IS0 8601 (YYYY-MM-DD).
- **``Accommodations``**: (``list``) ``Opcional``. Listado de alojamientos a añadir al carrito.
    - **``Accommodation``**: (``object``) ``Opcional``. Información del alojamiento.
        - **``EchoToken``**: (``string``) ``Requerido``. Token obtenido en la petición de alojamientos.
        - **``Rates``**: (``list``) ``Requerido``. Listado de identificadores de tarifas.
            - **``(string)``**:``Requerido``. Identificador de la tarifa.
- **``Packages``**: (``list``) ``Opcional``. Listado de agrupaciones de paquetes a añadir al carrito.
    - **``Package``**: (``object``) ``Opcional``. Información del grupo paquete.
        - **``EchoToken``**: (``string``) ``Requerido``. Token obtenido en la petición de paquetes.
        - **``Packages``**: (``list``) ``Requerido``. Listado de paquetes.
            - **``Package``**: (``object``) ``Requerido``. Información del paquete.
                - **``Id``**:``Requerido``. Identificador del paquete.

### Ejemplos

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/add.request.1.md"

## Estructura de la respuesta

Es relevante tener en cuenta las propiedades **``Id``** que son devueltas en la respuesta, dado que serán necesarios para manipular los productos una vez han sido añadidos al carrito.

- **`Success`**: (``boolean``). Indica si la llamada ha sido procesada satisfactoriamente.
- **`Activities`**: (``list``). Listado de las actividades añadidas en la **petición actual**. Si no se ha añadido actividades, esta propiedad no aparecerá.
    - **`Activity`**: (``object``). Información de la actividad añadida.
        - **`Id`**: (``string``). Identificador que se ha asignado a esta actividad dentro del carrito.
        - **`Activity`**: (``object``). Información de la actividad añadida.
            - **`ProductId`**: (``string``). Identificador de producto.
            - **`Quantity`**: (``string``). Cantidad añadida.
            - **`AccessDateTime`**: (``dateTime``). Fecha de acceso. Formato ISO 8601 (YYYY-MM-DDThh\:mm\:ss)
- **`Accommodations`**: (``list``). Listado de las alojamientos añadidos en la **petición actual**. Si no se ha añadido alojamientos, esta propiedad no aparecerá.
    - **`Accommodation`**: (``object``). Información del alojamiento añadido.
        - **`Id`**: (``string``). Identificador que se ha asignado a este alojamiento dentro del carrito.
        - **`RateId`**: (``string``). Identificador de la tarifa.

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/add.response.1.md"