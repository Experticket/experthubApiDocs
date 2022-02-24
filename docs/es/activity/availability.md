# Aforo disponible

Como se ha visto en la obtención del [catálogo](catalog.md), tanto los `ProductBases`como los `Products` tienen la propiedad `DaysWithLimitedCapacity`. De la misma manera las `Sessions` tienen el campo `HasLimitedCapacity`. De hecho, siguiendo el ejemplo, vemos que:

- El `ProductBase` "gfo753rgjfbw6" tiene marcado el 1 de Noviembre de 2001 como fecha en la que hay que consultar la disponibilidad.
- El `Product` "htgy4tgm9q21n" tiene marcados el 15 de agosto y el 17 de abril de 2001 como fechas en ls que hay que consultar la disponibilidad.
- El `Product` "q2oghu9mye7h2" tiene dos sesiones, ambas con `HasLimitedCapacity = true`, por lo que hay que consultar su disponibilidad.

!!! note "Notas aclaratorias"
    - Para los días definidos, se debe consultar el aforo disponible del `ProductBase` y/o `Product` antes de ofrecer el producto al cliente. Si se añade al carrito y se ha superado el aforo, al intentar confirmar la venta devolverá un error. Análogamente, para cada sesión con aforo limitado se debe consultar su disponibilidad antes de ofrecer el producto al cliente.
    - Si el campo `DaysWithLimitedCapacity` está vacío significa que no hay que consultar la disponibilidad para ninguna fecha.
    - El aforo concierne a los tickets de tipo aforo (`IsQuotaTicket == true`).
        - El aforo de un producto es la cantidad de tickets de tipo aforo que se pueden vender de ese producto. Siguiendo el ejemplo, el `Product` "htgy4tgm9q21n" está formado por tres tickets de tipo aforo. Así pues, si el aforo del producto fuera de 9, sólo se podrían vender 3 productos. Si el aforo fuera de 16, sólo se podrían vender 5 productos.
        - El aforo de un `ProductBase` es la cantidad de tickets de tipo aforo que se pueden vender de la suma de todos los productos del `ProductBase`. Siguiendo el ejemplo, el `ProductBase` "gfo753rgjfbw6" está formado por un producto ("ctgyir9m9q4bo") con un ticket de tipo aforo y otro producto ("htgy4tgm9q21n") con tres tickets de tipo aforo. Si el aforo del `ProductBase` fuera de 21, se podrían vender combinaciones como:
            - 21 productos de "ctgyir9m9q4bo" (21 x 1 = 21)
            - 7 productos de "htgy4tgm9q21n" (7 x 3 = 21)
            - 6 productos de "ctgyir9m9q4bo" y 5 de "htgy4tgm9q21n" (6 x 1 + 5 x 3 = 21)
            - 15 productos de "ctgyir9m9q4bo" y 3 de "htgy4tgm9q21n" (15 x 1 + 3 x 3 = 21)
            - Y cualquier otra combinación que se nos ocurra.

## Método de acceso

**POST** /availablecapacity

## Estructura de datos de envío

- **`ProductBaseIds`**: array de identificadores de categorías por las que filtrar.
- **`ProductIds`**: array de identificadores de productos por los que filtrar.
- **`SessionIds`**: array de identificadores de sesión por los que filtrar.
- **`Dates`**: array de fechas por ls que filtrar. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`FromDate`**: si no se quiere especificar `Dates`, se puede filtar por fecha de inicio. No permite valores anteriores al día de hoy. Su valor por defecto es el día de hoy. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`ToDate`**: si no se quiere especificar `Dates`, se puede filtrar por fecha de fin. Su valor por defecto es la fecha correspondiente a dentro de un año. *Formato ISO 8601 (yyyy-MM-dd)*.

!!! info
    Se debe definir al menos un `ProductBaseId` o un `ProductId`. Se pueden añadir tantos como se desee y se considerarán un ***OR***.

### Ejemplos de envío

--8<-- "includes/AvailabilityQueryExamples.md"

Consultar el aforo de un `ProductBaseId` para todas las fechas desde hoy hasta dentro de un año.

``` json
{
    "ProductBaseIds": [
        "dj48vjsyufvyu"
    ]
}
```

Consultar el aforo de varios `ProductBaseId` para todas las fechas desde hoy hasta dentro de un año.

``` json
{
    "ProductBaseIds": [
        "dj48vjsyufvyu",
        "ajr7v0alt62hl"
    ]
}
```

Consultar el aforo de un `ProductId` para todas las fechas desde hoy hasta dentro de un año.

``` json
{
    "ProductIds": [
        "dj48vjsyufvyu"
    ]
}
```

Consultar el aforo de varios `ProductId` para todas las fechas desde hoy hasta dentro de un año.

``` json
{
    "ProductIds": [
        "dj48vjsyufvyu",
        "ajr7v0alt62hl"
    ]
}
```

Consultar el aforo de un `SessionId` para todas las fechas desde hoy hasta dentro de un año.

``` json
{
    "SessionIds": [
        "dj48vjsyufvyu"
    ]
}
```

Consultar el aforo de varios `SessionId` para todas las fechas desde hoy hasta dentro de un año.

``` json
{
    "SessionIds": [
        "dj48vjsyufvyu",
        "ajr7v0alt62hl"
    ]
}
```

Consultar utilizando diferentes criterios, que funcionarán como un ***OR***.

``` json
{
    "ProductBaseIds": [
        "dj48vjsyufvyu",
        "ajr7v0alt62hl"
    ],
    "ProductIds": [
        "abc8vjsyufvyu",
        "1237v0alt62hl"
    ]
}
```

Consultar el aforo de un `ProductBaseId` para una fecha concreta.

``` json
{
    "ProductBaseIds": [
        "dj48vjsyufvyu"
    ],
    "Dates": [
        "2001-08-15"
    ]
}
```

Consultar el aforo de un `ProductBaseId` para un rango de fechas.

``` json
{
    "ProductBaseIds": [
        "dj48vjsyufvyu"
    ],
    "FromDate": "2001-08-01",
    "ToDate": "2001-08-31"
}
```

Se pueden realizar filtrados más complejos.

=== "Complex filter 1"

    ``` json
    {
        "ProductBaseIds": [
            "dj48vjsyufvyu",
            "ajr7v0alt62hl"
        ],
        "ProductIds": [
            "abc8vjsyufvyu",
            "1237v0alt62hl"
        ],
        "FromDate": "2001-08-01",
        "ToDate": "2001-08-31"
    }
    ```

=== "Complex filter 2"

    ``` json
    {
        "ProductBaseIds": [
            "dj48vjsyufvyu",
            "ajr7v0alt62hl"
        ],
        "ProductIds": [
            "abc8vjsyufvyu",
            "1237v0alt62hl"
        ],
        "Dates": [
            "2001-08-15",
            "2001-11-01"
        ]
    }
    ```

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
    - **`Date`**: fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **`AvailableCapacity`**: capacidad disponible para la venta.
- **`Success`**: booleano (true/false) que indica si la obtención de la disponibilidad ha sido correcta o no.
- **`Timestamp`**.
- **`ErrorMessage`**: mensaje de error explicando por qué la obtención de la disponibilidad no ha sido correcta. En caso que haya sido correcta, el campo no aparece.

### Ejemplo de respuesta

--8<-- "includes/AvailabilityResultExamples.md"

``` json
{
    "ProductsBases": [],
    "Products": [
        {
            "ProductId": "zqqucgr1njhfq",
            "Date": "2021-07-20",
            "AvailableCapacity": 0
        },
        {
            "ProductId": "zqqucgr1njhfq",
            "Date": "2021-07-22",
            "AvailableCapacity": 0
        },
        {
            "ProductId": "zqqucgr1njhfq",
            "Date": "2021-07-23",
            "AvailableCapacity": 99
        }
    ],
    "Sessions": [],
    "Success": true,
    "Timestamp": "2022-02-18T17:02:27.8165916"
}
```
