# Precios en tiempo real

Mediante este método podemos calcular los precios de uno o varios productos, para una o múltiples fechas de acceso.

!!! success ""
    Si el producto no tiene el campo **`RequiresRealTimePrice`** del [catálogo](catalog.md) definido a `#!csharp true` entonces no es necesario realizar esta llamada.

!!! warning ""
    Si el producto tiene el campo **`RequiresRealTimePrice`** del [catálogo](catalog.md) definido a `#!csharp true` entonces debemos realizar esta llamada cada vez que queramos ofrecer al cliente dicho producto para conocer su precio actual. En el [catálogo](catalog.md) se ofrece un precio base el cual puede sufrir alteraciones (aumento o descuento) en función de ciertos factores.

!!! info "¿Por qué hablamos de precio a tiempo real?"

    El precio de un producto depende del momento en que se hace la consulta del mismo. Existen factores como los días que faltan hasta la fecha de acceso o la temporada, que hacen que el precio varíe.

## Método de acceso

**POST** /realTimePrices

## Estructura de la petición

- **`ProductIds`**: array de identificadores de producto.
- **`AccessDates`**: array de fechas de entrada que queremos consultar. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`StartDate`**: inicio del rango de fechas de entrada que queremos consultar. Complementa a `AccessDates` y necesita que se especifique `EndDate`. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`EndDate`**: fin del rango de fechas de entrada que queremos consultar. Complementa a `AccessDates` y necesita que se especifique `StartDate`. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`CombinedProducts`**: array de productos combinados.
    - **`CombinedProductId`**: identificador del producto combinado.
    - **`Products`**: array de productos incluidos en el producto combinado.
        - **`ProductId`**: identificador del producto combinado.
        - **`AccessDate`**: fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.

### Ejemplos de petición

--8<-- "includes/examples/activity/realTimePricesQueryExamples.md"

## Estructura de la respuesta

- **`ProductsRealTimePrices`**: array de precios en tiempo real.
    - **`ProductId`**: identificador del producto.
    - **`AccessDate`**: fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **`Price`**: precio al que debe venderse el producto.
    - **`PriceMode`**: tipo de precio.

        ??? example "Posibles valores"
            - 1: PVP
            - 2: precio neto

    - **`CombinedProductId`**: identificador del producto combinado.
    - **`CombinedProductProducts`**: array de productos incluidos en el producto combinado.
        - **`ProductId`**: identificador del producto.
        - **`AccessDate`**: fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
    --8<-- "includes/responseBaseDocumentation.es.md"

--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplos de respuesta

--8<-- "includes/examples/activity/realTimePricesResponseExamples.md"
