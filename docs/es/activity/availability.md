# Aforo Disponible

Tal y como hemos visto en el punto [obtención de catálogo](catalog.md), tanto los ``ProductBases`` como los ``Products`` tienen la propiedad **``DaysWithLimitedCapacity``**, así como mediante la [llamada para obtener sesiones](sessions.md) vemos que ``Sessions`` pueden tener definido **``AvailableCapacity``**.

!!! success ""
    Si el campo ``DaysWithLimitedCapacity`` está vacío y, en caso de que el producto tenga sesiones no auto asignadas (véase en el [catálogo](catalog.md)), si las sesiones no tienen el campo ``AvailableCapacity`` definido significa que no hay que consultar la disponibilidad para ninguna fecha, por consiguiente no es necesario realizar está llamada al API.

!!! warning ""
    Si el campo ``DaysWithLimitedCapacity`` tiene días definidos o las sesiones tiene definido ``AvailableCapacity``, debemos consultar el aforo disponible de la categoría (ProductBase), del producto, y/o de la sesión que corresponda antes de ofrecer el producto al cliente.

!!! error ""
    Si al intentar confirmar el carrito se ha superado el aforo, es decir, no queda aforo suficiente para llevar a cabo la reserva, se devolverá un error.

El aforo concierne a los tickets de tipo aforo (``#!chsarp IsQuotaTicket == true``). Por tanto, el aforo de un producto es la cantidad de tickets de tipo aforo que se pueden vender de ese producto. Y el aforo de un ProductBase es la cantidad de tickets de tipo aforo que se pueden vender de la suma de todos los productos del ProductBase.

??? info "Ejemplo"
    Obteniedno la siguiente información del catálogo:

    - El siguiente ``ProductBase`` tiene marcado el 1 de Noviembre de 2022 como fecha en la que hay que consultar la disponibilidad.

        ``` json hl_lines="3"
        {
            "ProductBaseId": "gfo753rgjfbw6",
            "DaysWithLimitedCapacity": "2022-11-01"
        }
        ```
    - El siguiente ``Product`` tiene marcados el 15 de agosto y el 17 de abril de 2022 como fechas en la que hay que consultar la disponibilidad.

        ``` json hl_lines="3"
        {
            "ProductId": "htgy4tgm9q21n",
            "DaysWithLimitedCapacity": "2022-04-17,2022-08-15"
        }
        ```
    - El siguiente ``Product`` tiene dos sesiones, ambas con ``AvailableCapacity`` definido, por tanto hay que consultar su disponibilidad.

        ``` json hl_lines="7"
        {
            "ProductId": "q2oghu9mye7h2",
            "Tickets": [
                {
                    "TicketId": "fb8mcqxyo22rg",
                    "IsQuotaTicket": true,
                    "TicketEnclosureId": "g5u6m3xew6hxy"
                }
            ]
        }
        ```
        ``` json hl_lines="5 6 7"
        {
            "TicketEnclosureId": "g5u6m3xew6hxy",
            "Sessions": 
            {
                "SessionContentProfileId ": "dkjvidkfjkdfv",
                "SessionGroupProfileId": "dfjbfqwe8934d",
                "TicketEnclosureAutoAssignSessionType": 0
            }
        }
        ```

        Al [obtener las sesiones](sessions.md) vemos lo siguiente:

        ``` json hl_lines="6 11"
        {
        "Sessions": [
            {
                "SessionId": "5b8qkqnmhdmk1",
                "SessionTime": "2021-06-21T10:00:00",
                "AvailableCapacity": 165
            },
            {
                "SessionId": "5o3bwhx1ze1m1",
                "SessionTime": "2021-09-06T10:00:00",
                "AvailableCapacity": 230
            },
            {
                "SessionId": "sdviufdnvr843",
                "SessionTime": "2021-09-06T17:00:00"
            }
        ]
        }
        ```

    - El siguiente ``Product`` está formado por tres tickets de tipo aforo. Así pues, si el aforo del producto fuera de 9, solo podríamos vender 3 productos. Y si el aforo fuera de 16, solo podríamos vender 5 productos.

        ``` json hl_lines="6 10 14"
        {
            "ProductId": "htgy4tgm9q21n",
            "Tickets": [
                {
                    "TicketId": "1tqgtrf7ctefc",
                    "IsQuotaTicket": true
                }, 
                {
                    "TicketId": "2lob55g8w3fff",
                    "IsQuotaTicket": true
                }, 
                {
                    "TicketId": "jkp78j40cnfh3",
                    "IsQuotaTicket": true
                }, 
                {
                    "TicketId": "gggsijt911am4",
                    "IsQuotaTicket": false
                }
            ]
        }
        ```
    - El siguiente ``ProductBase`` está formado por un producto con un ticket de tipo aforo y otro producto con tres tickets de tipo aforo:

        ``` json hl_lines="10 14 18 31"
        {
            "ProductBaseId": "gfo753rgjfbw6",
            "DaysWithLimitedCapacity": "2022-08-31",
            "Products": [
                {
                    "ProductId": "htgy4tgm9q21n",
                    "Tickets": [
                        {
                            "TicketId": "1tqgtrf7ctefc",
                            "IsQuotaTicket": true
                        }, 
                        {
                            "TicketId": "2lob55g8w3fff",
                            "IsQuotaTicket": true
                        }, 
                        {
                            "TicketId": "jkp78j40cnfh3",
                            "IsQuotaTicket": true
                        }, 
                        {
                            "TicketId": "gggsijt911am4",
                            "IsQuotaTicket": false
                        }
                    ]
                },
                {
                    "ProductId": "q2oghu9mye7h2",
                    "Tickets": [
                        {
                            "TicketId": "fb8mcqxyo22rg",
                            "IsQuotaTicket": true
                        }
                    ]
                }
            ]
        }
        ```

        Así pues, si el aforo del ``ProductBase`` fuera de 21, podríamos vender combinaciones como las siguientes:

          - 21 productos de "q2oghu9mye7h2" (21 x 1 = 21)
          - 7 productos de "htgy4tgm9q21n" (7 x 3 = 21)
          - 6 productos de "q2oghu9mye7h2" y 5 de "htgy4tgm9q21n" (6 x 1 + 5 x 3 = 21)
          - 15 productos de "q2oghu9mye7h2" y 3 de "htgy4tgm9q21n" (15 x 1 + 3 x 3 = 21)
          - Y cualquier otra combinación que se nos ocurra.

## Método de acceso

**POST** /availablecapacity

## Estructura de datos de envío

- **`ProductBaseIds`**: array de identificadores de categorías por las que filtrar.
- **`ProductIds`**: array de identificadores de productos por los que filtrar.
- **`SessionIds`**: array de identificadores de sesión por los que filtrar.
- **`Dates`**: array de fechas por las que filtrar. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`FromDate`**: si se quiere filtrar mediante un rango de fechas, se puede filtar por fecha de inicio. No permite valores anteriores al día de hoy. Su valor por defecto es el día de hoy. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`ToDate`**: si se quiere filtrar mediante un rango de fechas, se puede filtrar por fecha de fin. Su valor por defecto es la fecha correspondiente a dentro de un año. *Formato ISO 8601 (yyyy-MM-dd)*.

!!! tip "Importante"
    Se debe definir al menos un `ProductBaseId`, un `ProductId` o un `SessionId`. Se pueden añadir tantos como se desee y se considerarán un ***OR***.

### Ejemplos de envío

--8<-- "includes/examples/activity/availabilityQueryExamples.md"

## Estructura de datos de respuesta

- **`ProductBases`**: array que contiene los `ProductBase` solicitados. Corresponde a cada día con acceso limitado de cada uno de los `ProductBase`.
    - **`ProductBaseId`**: identificador del `ProductBase`.
    - **`Date`**: fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **`AvailableCapacity`**: capacidad disponible para la venta.
- **`Products`**: array que contiene los productos solicitados. Corresponde a cada día con acceso limitado de cada uno de los productos.
    - **`ProductId`**: identificador del producto.
    - **`Date`**: fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **`AvailableCapacity`**: capacidad disponible para la venta.
- **`Sessions`**: array que contiene las sesiones solicitadas. Corresponde a cada día con acceso limitado de cada una de las sesiones.
    - **`SessionId`**: identificador de la sesión.
    - **`Date`**: fecha de acceso. *Formato ISO 8601 (yyyy-MM-ddThh:mm:ss.fffffff)*.
    - **`AvailableCapacity`**: capacidad disponible para la venta.
- **`Success`**: booleano (``#!csharp true/false``) que indica si la obtención de la disponibilidad ha sido correcta o no.
- **`Timestamp`**: indica el momento de la obtención de la respuesta. *Formato ISO 8601 (yyyy-MM-ddThh:mm:ss.fffffff)*.
- **`ErrorMessage`**: mensaje de error explicando por qué la obtención de la disponibilidad no ha sido correcta. En caso que haya sido correcta, el campo no aparece.

### Ejemplo de respuesta

--8<-- "includes/examples/activity/availabilityResponseExamples.md"
