# Reserva de productos

Este método permite reservar los productos añadidos al carrito de la compra durante un periodo de tiempo.

Una vez que se ha confirmado la reserva, ya no es posible añadir más productos al carrito.

## Método de acceso

**POST** /ShoppingCart/Confirm

## Estructura de la petición

- **``ShoppingCartId``**: (``string``) ``Requerido``. Identificador del carrito.

### Ejemplos de llamadas

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/confirm.request.1.md"

## Estructura de la respuesta

- **`ExpirationDateTime`**: (``dateTime``). Indica cuándo la reserva expirará. Formato IS0 8601 (YYYY-MM-DDThh\:mm\:ss.d).
- **`Activities`**: (``object``). Información sobre la actividad añadida.
    - **`Products`**: (``list``). Listado de productos añadidos.
        - **`ProductId`**: (``string``). Identificador del producto añadido.
        - **`ProductName`**: (``string``). Nombre del producto añadido.
        - **`AccessDateTime`**: (``dateTime``). Fecha y hora de acceso. Formato IS0 8601 (YYYY-MM-DDThh\:mm\:ss.d).
        - **``Price``**: (``decimal``). Precio de la tarifa.
        - **``PriceMode``**: (``int``). Tipo de precio.

            ??? example "Posibles valores"
                --8<-- "includes/enum/priceMode.md"

        - **``Success``**: (``boolean``). Si ha sido correctamente reservado.
        - **``Tickets``**: (``list``). Listado de tickets que conforman este producto.
            - **``Ticket``**: (``object``). Información sobre el ticket.
                - **``TicketId``**: (``string``). Identificador del ticket.
        - **`CancellationPolicy`**: (``object``). Indica las políticas de cancelación que se aplican al cancelar este producto.
            - **`IsRefundable`**: (``boolean``). Indica si la cancelación gratuita está disponible en algún momento.
            - **`Rules`**: (``list``). Listado de reglas que se aplican al efectuar la cancelación.
                - **`Rule`**: Información sobre la regla a aplicar.
                    - **`HoursInAdvanceOfAccess`**: (``int``). Indica la cantidad de horas de antelación con respecto a la fecha de acceso a partir de las cuales se aplicará la penalización de precio indicada en `Percentage`.
                    - **`Percentage`**: (``decimal``). Porcentaje de penalización sobre el precio de la entrada.
                    - **`Amount`**: (``decimal``). Valor total de la penalización que se aplicará.
                    - **`FromInclusiveDateTime`**: (``dateTime``). Fecha/hora a partir de la cual se aplicará esta regla.
                    - **`ToExclusiveDateTime`**: (``dateTime``). Fecha/hora hasta la cual se aplicará esta regla.

- **`Accommodations`**: (``list``). Información sobre los alojamientos/habitaciones añadidas al carrito.
    - **`Accommodation`**: (``object``). Información sobre el alojamiento.
        - **`ProductId`**: (``string``). Identificador de la tarifa.
        - **`ProductConditions`**: (``string``). Condiciones del producto.
        - **`AccessDateTime`**: (``dateTime``). Fecha de entrada.
        - **`AccessEndDateTime`**: (``dateTime``). Fecha de salida.
        - **`Quantity`**: (``int``). Cantidad de unidades añadidas.
        - **``Price``**: (``decimal``). Precio de la tarifa.
        - **``PriceMode``**: (``int``). Tipo de precio.

            ??? example "Posibles valores"
                --8<-- "includes/enum/priceMode.md"

        - **``Success``**: (``boolean``). Si ha sido correctamente reservado.
        - **``ErrorMessage``**: (``boolean``). En caso de error en la reserva, mensaje asociado.
        - **``ChildrenAges``**: (``list``). Listado con las edades de los bebés/niños.
            - **``int``**: Edad del bebé/niño
        - **``NumberOfAdults``**: (``int``). Número de adultos en esta habitación.
        - **``NumberOfChildren``**: (``int``). Número de niños en esta habitación.
        - **``NumberOfSenior``**: (``int``). Número de _seniors_ en esta habitación.
        - **``NumberOfBabies``**: (``int``). Número de bebés en esta habitación.
        - **``NumberOfGeneric``**: (``int``). Número de personas (sin definir) en esta habitación.
        - **`CancellationPolicy`**: (``object``). Indica las políticas de cancelación que se aplican al cancelar este producto.
            - **`IsRefundable`**: (``boolean``). Indica si la cancelación gratuita está disponible en algún momento.
            - **`Rules`**: (``list``). Listado de reglas que se aplican al efectuar la cancelación.
                - **`Rule`**: Información sobre la regla a aplicar.
                    - **`HoursInAdvanceOfAccess`**: (``int``). Indica la cantidad de horas de antelación con respecto a la fecha de acceso a partir de las cuales se aplicará la penalización de precio indicada en `Percentage`.
                    - **`Percentage`**: (``decimal``). Porcentaje de penalización sobre el precio de la entrada.
                    - **`Amount`**: (``decimal``). Valor total de la penalización que se aplicará.
                    - **`FromInclusiveDateTime`**: (``dateTime``). Fecha/hora a partir de la cual se aplicará esta regla.

- **`PaymentMethodsNotApplicable`**: (``boolean``). Indica si los método de pago serán aplicables o no a este colaborador. Los colaboradores con contrato "débito" tendrán que aplicar los métodos de pago (`#!csharp PaymentMethodsNotApplicable = false`).
- **`PaymentMethods`**: (``list``). Métodos de pago soportados para el colaborador en caso de ser a débito.
    - **`PaymentMethod`**: (``object``). Información sobre el método de pago.
        - **`Type`**: (``int``). Identificador del método de pago.
        - **`Name`**: (``string``). Nombre del método de pago.
        - **`EnableSendByEmail`**: (``boolean``). En algunos casos, es posible que el cliente pueda realizar el cobro desde un enlace que se le hace llegar por email. En tal caso se indicará, en esta propiedad, de tal opción.

--8<-- "includes/experthubResponseBaseDocumentation.es.md"

### Ejemplos de respuestas

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/confirm.response.1.md"
