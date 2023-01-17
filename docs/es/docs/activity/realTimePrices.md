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

- **`ProductIds`**: (``list``). Array de identificadores de producto.
    - **``(string)``**: Identificador del producto.
- **`AccessDates`**: (``string``). Array de fechas de entrada que queremos consultar. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **``(date)``**: Fechas a consultar.
- **`StartDate`**: (``date``). Inicio del rango de fechas de entrada que queremos consultar. Complementa a `AccessDates` y necesita que se especifique `EndDate`. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`EndDate`**: (``date``). Fin del rango de fechas de entrada que queremos consultar. Complementa a `AccessDates` y necesita que se especifique `StartDate`. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`CombinedProducts`**: (``list``). Array de productos combinados.
    - **`CombinedProductId`**: (``string``). Identificador del producto combinado.
    - **`Products`**: (``list``). Array de productos incluidos en el producto combinado.
        - **`ProductId`**: (``string``). Identificador del producto combinado.
        - **`AccessDate`**: (``date``). Fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.

### Ejemplos de petición

--8<-- "includes/examples/activity/realTimePricesQueryExamples.md"

## Estructura de la respuesta

- **`ProductsRealTimePrices`**: (``list``). Array de precios en tiempo real.
    - **`ProductId`**: (``string``). Identificador del producto.
    - **`AccessDate`**: (``date``). Fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **`Price`**: (``decimal``). Precio al que debe venderse el producto.
    - **`PriceMode`**: (``byte``). Tipo de precio.

        ??? example "Posibles valores"
            - 1: PVP
            - 2: precio neto

    - **`CombinedProductId`**: (``string``). Identificador del producto combinado.
    - **`CombinedProductProducts`**: (``string``). Array de productos incluidos en el producto combinado.
        - **`ProductId`**: (``string``). Identificador del producto.
        - **`AccessDate`**: (``date``). Fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
    --8<-- "includes/responseBaseDocumentation.es.md"

--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplos de respuesta

--8<-- "includes/examples/activity/realTimePricesResponseExamples.md"
