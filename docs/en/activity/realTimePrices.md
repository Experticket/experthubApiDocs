# Precios en tiempo real

Mediante este método podemos calcular los precios de uno o varios productos, para una o múltiples fechas de acceso.

!!! info "¿Por qué hablamos de tiempo real?"

    El precio de un producto depende del momento en que se hace la consulta del mismo. Existen factores como los días que faltan hasta la fecha de acceso o la temporada, que hacen que el precio varíe.

Es necesario realizar esta llamada cada vez que queramos averiguar el precio de un producto para una fecha en concreto. El precio que tiene hoy la entrada a un parque para dentro de un mes no tiene por qué ser el mismo mañana.

## Método de acceso

**POST** /realTimePrices

## Estructura de datos de envío

Para obtener los precios en tiempo real debe especificarse la siguiente estructura de datos en el cuerpo del método.

- **`ProductIds`**: lista identificadores de producto.
- **`AccessDates`**: lista fechas de entrada que queremos consultar. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`StartDate`**: inicio del rango de fechas de entrada que queremos consultar. Complementa a `AccessDates` y necesita que se especifique `EndDate`. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`EndDate`**: fin del rango de fechas de entrada que queremos consultar. Complementa a `AccessDates` y necesita que se especifique `StartDate`. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`CombinedProducts`**: array de productos combinados.
    - **`CombinedProductId`**: identificador del producto combinado.
    - **`Products`**: array de productos incluidos en el producto combinado.
        - **`ProductId`**: identificador del producto combinado.
        - **`AccessDate`**: fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.

### Ejemplos de envío

--8<-- "includes/RealTimePricesQueryExamples.md"
=== "ProductIds"

    ``` json
    {
        "ProductIds": [
            "dj48vjsyufvyu",
            "ajr7v0alt62hl"
        ],
        "AccessDates": [
            "2020-01-02",
            "2022-05-15"
        ]
    }
    ```

## Estructura de datos de respuesta

- **`ProductsRealTimePrices`**: array de precios en tiempo real.
    - **`ProductId`**: identificador del producto.
    - **`AccessDate`**: fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **`Price`**: precio al que debe venderse el producto.
    - **`PriceMode`**: tipo de precio. Opciones:
        - 1: PVP
        - 2: precio neto
    - **`CombinedProductId`**: identificador del producto combinado.
    - **`CombinedProductProducts`**: array de productos incluidos en el proucto combinado.
        - **`ProductId`**: identificador del producto.
        - **`AccessDate`**: fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **`Success`**: booleano (true/false) que indica si la obtención del precio en tiempo real de este proucto ha sido correcta o no.
    - **`ErrorMessage`**: mensaje de error explicando por qué la obtención del precio en tiempo real de este producto no ha sido correcta. En caso que haya sido correcta, el campo no aparece.
- **`Success`**: booleano (true/false) que indica si la obtención de los precios en tiempo real ha sido correcta o no.
- **`Timestamp`**. *ISO 8601 format (yyyy-MM-ddThh:mm:ss.fffffff)*
- **`ErrorMessage`**: mensaje de error explicando por qué la obtención de los precios en tiempo real no ha sido correcta. En caso que haya sido correcta, el campo no aparece.

### Ejemplos de respuesta

--8<-- "includes/RealTimePricesResultExamples.md"
=== "ProductIds"

    ``` json
    {
        "ProductsRealTimePrices": [
            {
                "ProductId": "dj48vjsyufvyu",
                "AccessDate": "2020-01-02",
                "Price": 29,
                "PriceMode": 1,
                "Success": true
            },
            {
                "ProductId": "dj48vjsyufvyu",
                "AccessDate": "2022-05-15",
                "Price": 35,
                "PriceMode": 1,
                "Success": true
            },
            {
                "ProductId": "ajr7v0alt62hl",
                "AccessDate": "2020-01-02",
                "Price": 18,
                "PriceMode": 1,
                "Success": true
            },
            {
                "ProductId": "ajr7v0alt62hl",
                "AccessDate": "2022-05-15",
                "Price": 22,
                "PriceMode": 1,
                "Success": true
            }
        ],
        "Success": true,
        "Timestamp": "2022-02-18T17:02:27.8165916"
    }
    ```
