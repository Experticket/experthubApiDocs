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
        - **``CombinedProductId``**: (``string``) ``Opcional``. Identificador del producto combinado.
        - **``AccessDateTime``**: (``date``) ``Requerido``. Fecha de acceso. Formato IS0 8601 (YYYY-MM-DD).
        - **``Quantity``**: (``int``) ``Requerido``. Cantidad de productos.
        - **``Tickets``**: (``object``) ``Opcional``. Lista con la información del ticket.
            - **``TicketId``**: (``string``) ``Requerido``. Identificador del ticket.
            - **``SessionId``**: (``string``) ``Opcional``. Identificador de la sesión.
            - **``AccessDateTime``**: (``date``) ``Requerido``. Fecha de acceso. Formato IS0 8601 (YYYY-MM-DD).
            - **``Questions``**: (``object``) ``Opcional``. Identificador del ticket.
                - **``TicketQuestionId``**: (``string``) ``Requerido``. Identificador de la pregunta.
                - **``StringValue``**: (``string``) ``Requerido``. Respuesta de la pregunta.

            ??? example "Posibles valores"
                --8<-- "includes/enum/examenResponseQuestions.md"

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
                - **``Providers``**: (``list``) ``Opcional``. Objeto con los datos del proveedor.
                    - **``Id``**: (``string``) ``Requerido``. Identificador.
                    - **``Activities``**: (``list``) ``Opcional``. Listado de actividades a añadir al carrito.
                        - **``Id``**: (``string``) ``Requerido``. Identificador.
                        - **``ProductBaseId``**: (``string``) ``Requerido``. Identificador del producto base.
                        - **``Tickets``**: (``object``) ``Opcional``. Lista con la información del ticket.
                            - **``SessionId``**: (``string``) ``Opcional``. Identificador de la sesión.
                            - **``AccessDateTime``**: (``date``) ``Requerido``. Fecha de la sesión.
                            - **``TicketId``**: (``string``) ``Opcional``. Identificador del ticket.


### Ejemplos de llamadas

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/add.request.1.md"

## Estructura de la respuesta

Es relevante tener en cuenta las propiedades **``Id``** que son devueltas en la respuesta, dado que serán necesarios para manipular los productos una vez han sido añadidos al carrito.

- **`Activities`**: (``list``). Listado de las actividades añadidas en la **petición actual**. Si no se ha añadido actividades, esta propiedad no aparecerá.
    - **`Activity`**: (``object``). Información de la actividad añadida.
        - **`Id`**: (``string``). Identificador que se ha asignado a esta actividad dentro del carrito.
        - **`Activity`**: (``object``). Información de la actividad añadida.
            - **`ProductId`**: (``string``). Identificador de producto.
            - **`Quantity`**: (``int``). Cantidad añadida.
            - **`AccessDateTime`**: (``dateTime``). Fecha de acceso. Formato ISO 8601 (YYYY-MM-DDThh\:mm\:ss).
            - **`ForceNotAutoAssignSeating`**: (``boolean``). Forzar los asientos asignados.
            - **`Tickets`**: (``list``). Lista de tickets.
                - **`TicketId`**: (``string``). Identificador del ticket.
                - **`SessionId`**: (``string``). Identificador de la sesión.
                - **`Questions`**: (``object``). Información sobre las preguntas.
                    - **`TicketQuestionId`**: (``string``). Identificador de la pregunta.
                    - **`StringValue`**: (``string``). Respuesta de la pregunta.

- **`Accommodations`**: (``list``). Listado de los alojamientos añadidos en la **petición actual**. Si no se ha añadido alojamientos, esta propiedad no aparecerá.
    - **`Accommodation`**: (``object``). Información del alojamiento añadido.
        - **`Id`**: (``string``). Identificador que se ha asignado a este alojamiento dentro del carrito.
        - **`RateId`**: (``string``). Identificador de la tarifa.

--8<-- "includes/experthubResponseBaseDocumentation.es.md"

### Ejemplos de respuestas

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/add.response.1.md"
