# Catálogo básico de alojamiento

Este método nos permite obtener la información mínima e indispensable sobre los distintos alojamientos. Puede utilizarse, por ejemplo, para crear una página inicial de búsqueda.

El resultado será un listado de los distintos alojamientos disponibles según los filtros de búsqueda.

## Método de acceso

**POST** /Accommodation/BasicCatalog

## Estructura de la petición

--8<-- "includes/catalog/query/people.es.md"

--8<-- "includes/catalog/query/basicAccommodationItem.es.md"

--8<-- "includes/catalog/query/sort.es.md"

--8<-- "includes/catalog/query/paging.es.md"

### Ejemplos de llamadas

??? tip "Ejemplo: 2 habitaciones: "1 adulta + 1 niño" y "1 adulto""

--8<-- "includes/examples/accommodation/basicCatalog.request.1.md"

??? tip "Ejemplo: 1 habitación: "1 adulto + 1 niño" en alojamiento 3*"

--8<-- "includes/examples/accommodation/basicCatalog.request.2.md"