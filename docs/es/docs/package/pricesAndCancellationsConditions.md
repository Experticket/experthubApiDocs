# Disponibilidad de fechas

Este método nos permite obtener un listado de precios para cada paquete y grupo solicitados.

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

??? tip "Example"
    
    --8<-- "includes/examples/package/pricesAndCancellationsConditions.request.1.md"

## Estructura de la respuesta

- **``PaxGroupingsDates``**: (``list``). Listado de agrupaciones.
    - **``PaxGroupingDates``**: (``object``). Información de la agrupación.
        - **``Id``**: (``string``). Identificador de la agrupación (``PaxGroupingId``).
        - **``Dates``**: (``list``). Listado de fechas disponibles.
            - **``(date)``**: Fecha con disponibilidad. Formato IS0 8601 (YYYY-MM-DD). 

### Ejemplos

??? tip "Example"
    
    --8<-- "includes/examples/package/availableDates.response.1.md"