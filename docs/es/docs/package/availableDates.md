# Disponibilidad de fechas

Este método nos permite obtener la disponibildiad de fechas para un paquete específico.

## Método de acceso

**POST** /Package/AvailableDates

## Estructura de la petición

- **``EchoToken``**: (``string``). Token que identifica a la secuencia de peticiones. Ver [catálogo extendido](../extendedCatalog#estructura-de-la-respuesta)
- **``PackageId``**: (``string``). Identificador del paquete. Ver la propiedad ``Packages.Package.Id`` de [catálogo extendido](../extendedCatalog#estructura-de-la-respuesta)

### Ejemplos

??? tip "Example"
    
    --8<-- "includes/examples/package/availableDates.request.1.md"

## Estructura de la respuesta

- **``PaxGroupingsDates``**: (``list``). Listado de agrupaciones.
    - **``PaxGroupingDates``**: (``object``). Información de la agrupación.
        - **``Id``**: (``string``). Identificador de la agrupación (``PaxGroupingId``).
        - **``Dates``**: (``list``). Listado de fechas disponibles.
            - **``(date)``**: Fecha con disponibilidad. Formato IS0 8601 (YYYY-MM-DD). 

### Ejemplos