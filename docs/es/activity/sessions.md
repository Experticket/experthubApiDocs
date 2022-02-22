# Sesiones

Una sesión está definida por una fecha, un hora, un contenido y, opcionalmente, el aforo disponible.

Según esta definición, se entiende que una misma sesión puede ser compartida por varios tickets. Los tickets "Entrada adulto", "Entrada niño", "Entrada junior", "Entrada senior" y "Entrada discapacitado" pueden tener asociadas las mismas sesiones durante el año en curso (por ejemplo, 10 sesiones al día durante los 365 días al año).

Como esta casuística puede ser habitual, se ha procurado separar lo máximo posible la estructura de sesiones del catálogo de productos. Siguiendo con el ejemplo anterior, si se definiesen las sesiones en el catálogo de productos tendríamos 10 sesiones x 365 días = 3650 sesiones para cada uno de los 5 tickets ("Entrada adulto, "Entrada niño", "Entrada junior", "Entrada senior" y "Entrada discapacitado").

Por lo tanto, se define la estructura de sesiones, para minimizar la carga de datos y jerarquizar lo mejor posible el catálogo de sesiones.

## Método de acceso

**POST** /sessions

## Estructura de datos de envío

Para obtener las sesiones podemos utilizar diferentes filtros en el cuerpo del método. Cada filtro se considerará un ***AND***.

Debe especificarse la siguiente estructura de datos en el cuerpo del método.

- **`SessionsGroupProfileIds`**: lista de perfiles de grupos de sesión.
- **`SessionsGroupIds`**: lista de grupos de sesión.
- **`SessionContentProfileIds`**: lista de perfiles de contenido de sesión.
- **`FromDate`**: filtrado por fecha de inicio. No permite valores menores al día de hoy. El valor por defecto es el día actual. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`ToDate`**: filtrado por fecha de fin. Su valor por defecto es l fecha correnpondiente a dentro de un año. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`Dates`**: lista fechas por las que filtrar. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`LanguageCode`**: código del idioma de los contenidos.

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
- **`Timestamp`**.
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
