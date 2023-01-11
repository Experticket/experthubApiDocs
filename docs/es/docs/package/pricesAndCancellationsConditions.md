# Disponibilidad de fechas

Este método nos permite obtener un listado de precios para el conjunto de paquete, grupo y fecha solicitadas.

La definición de las agrupaciones (``PaxGroupings``) toma relevancia cuando el paquete consta de varias actividades y, por tanto, posibles diferentes fechas para la realización de cada una de las actividades.

## Método de acceso

**POST** /Package/PricesAndCancellationConditions

## Estructura de la petición

- **``EchoToken``**: (``string``). Token que identifica a la secuencia de peticiones. Ver [catálogo extendido](../extendedCatalog#estructura-de-la-respuesta)
- **``Packages``**: (``list``). Listado de paquetes a solicitar.
    - **``Package``**: (``object``). Información del paquete.
        - **``Id``**: (``string``). Identificador del paquete.
        - **``PaxGroupings``**: (``list``). Listado de agrupaciones.
            - **``PaxGrouping``**: (``object``). Información de la agrupación.
                - **``Id``**: (``string``). Identificador de la agrupación.
                - **``AccessDate``**: (``date``). Fecha de inicio de la actividad. Formato IS0 8601 (YYYY-MM-DD).

### Ejemplos

??? tip "Ejemplos"
    
    --8<-- "includes/examples/package/pricesAndCancellationsConditions.request.1.md"

## Estructura de la respuesta

- **``EchoToken``**: (``string``). Token que identifica a la secuencia de peticiones. Ver [catálogo extendido](../extendedCatalog#estructura-de-la-respuesta)
- **``Success``**: (``boolean``). Indica si la solicitud se ha podido satisfacer correctamente.
- **``Packages``**: (``list``). Listado de paquetes solicitados en la petición.
    - **``Package``**: (``object``). Información del paquete.
        - **``Id``**: (``string``). Identificador del paquete.
        - **``Price``**: (``decimal``). Precio del paquete.
        - **``PriceMode``**: (``int``). Tipo de precio.

            ??? example "Posibles valores"
                --8<-- "includes/enum/priceMode.md"

        - **``Commission``**: (``object``). Información sobre la comisión.
            - **``Type``**: (``int``). Tipo de comisión

                ??? example "Posibles valores"
                    --8<-- "includes/enum/comissionType.md"

            - **``Value``**: (``decimal``). Valor de la comisión.

### Ejemplos

??? tip "Ejemplos"
    
    --8<-- "includes/examples/package/pricesAndCancellationsConditions.response.1.md"