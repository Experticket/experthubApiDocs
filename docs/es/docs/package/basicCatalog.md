# Catálogo básico de paquetes

Este método nos permite obtener la información mínima e indispensable sobre los distintos paquetes. Puede utilizarse, por ejemplo, para crear una página inicial de búsqueda.

El resultado será una matriz de las distintas actividades (``PrePackageIds``) y de los alojamientos disponibles para cada una de esas actividades.

Las actividades pueden tener ninguna, una o varias restricciones de alojamientos configurados internamente, como, por ejemplo, únicamente poder empaquetarse con un alojamiento específico o una restricción de distancia máxima al recinto. Estas restricciones pueden provocar que, aunque haya alojamientos en la zona o radio específicos, no aparezcan en la lista de resultados de paquetes (``Packages``).

## Método de acceso

**POST** /Package/BasicCatalog

## Estructura de la petición

--8<-- "includes/catalog/query/people.es.md"

--8<-- "includes/catalog/query/activity.es.md"

- **``Accomodation``**: (``object``) ``Requerido``. Información sobre los alojamientos a obtener.
    --8<-- "includes/catalog/query/basicAccommodationItem.es.md"

--8<-- "includes/catalog/query/filter.es.md"

    - **``DistanceRanges``**: (``list``) ``Opcional``. Listado de rangos de distancia con respecto a la actividad. En caso de más de un elemento, actuarán como un operador de unión ``OR``.
        - **``DistanceRange``**: (``object``) ``Opcional``. Rango de distancia con respecto a la actividad en metros.
            - **``Min``**: (``int``) ``Opcional``. Distancia mínima.
            - **``Max``**: (``int``) ``Opcional``. Distancia máxima.


--8<-- "includes/catalog/query/sort.es.md"

--8<-- "includes/catalog/query/paging.es.md"

### Ejemplos de llamadas

??? tip "Ejemplo: 2 habitaciones: "1 adulta + 1 niño" y "1 adulto""

--8<-- "includes/examples/package/basicCatalog.request.1.md"

??? tip "Ejemplo: 1 habitación: "1 adulto + 1 niño" en alojamiento 3*"

--8<-- "includes/examples/package/basicCatalog.request.2.md"

## Estructura de la respuesta

- **``TotalPages``**: (``int``). Número total de páginas.
- **``Packages``**: (``list``). Listado de paquetes con base en los criterios de búsqueda: Actividad/es, Alojamiento/s y Filtros.
    - **``Package``**: (``object``). Información del paquete.
        - **``Accommodation``**: (``object``). Información del alojamiento.
            - **``DistanceToActivity``**: (``decimal``). Distancia, en metros, desde el alojamiento hasta el punto inicial de la actividad.
            - **``MainImageUrl``**: (``string``). Url de la imagen principal del alojamiento.
            - **``Name``**: (``string``). Nombre del alojamiento.
            - **``Description``**: (``string``). Descripción del alojamiento.
            - **``Address``**: (``string``). Dirección del alojamiento.
            - **``City``**: (``string``). Ciudad donde se ubica el alojamiento.
            - **``PostalCode``**: (``string``). Código postal del alojamiento.
            - **``Country``**: (``string``). País donde está ubicado el alojamiento.
            - **``Type``**: (``string``). Tipo de alojamiento.

                ??? example "Posibles valores"
                    --8<-- "includes/enum/accommodationType.md"

            - **``Category``**: (``string``). Categoría del alojamiento.

                ??? example "Posibles valores"
                    --8<-- "includes/enum/accommodationCategory.md"

        - **``PriceFrom``**: (``decimal``). Precio de la combinatoria más baja para el paquete en cuestión.

--8<-- "includes/experthubResponseBaseDocumentation.es.md"

### Ejemplos de respuesta

??? tip "Example"
    --8<-- "includes/examples/package/basicCatalog.response.1.md"
