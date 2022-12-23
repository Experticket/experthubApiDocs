# Catálogo básico de paquetes

Este método nos permite obtener la información mínima e indispensable sobre los distintos paquetes. Puede utilizarse, por ejemplo, para crear una página inicial de búsqueda.

El resultado será una matriz de las distintas actividades (``PrePackageIds``) y de los alojamientos disponibles para cada uno de esas actividades. 

Las actividades pueden tener ninguna, una o varias restricciones de alojamientos configurados internamente, como por ejemplo, únicamente poder empaquetarse con un alojamiento específico o una restricción de distancia máxima al recinto. Esta restricción puede provocar que, aunque haya hoteles en la zona o radio específicos, no aparecer en la lista de resultados de paquetes (``Packages``).

## Método de acceso

**POST** /Package/BasicCatalog

## Estructura de la petición

- **``People``**: (``list``) ``Requerido``. Listado de personas que componen el paquete. El orden en el cual se añaden las personas repercute, posteriormente, en el índice a usar en la propiedad ``Room`` 
    - **``Person``**: (``object``) ``Requerido``. Información de la persona.
        - **``Type``**: (``int``) ``Requerido``. Tipo de persona.

            ??? example "Posibles valores"
                --8<-- "includes/enum/personType.md"

        - **``Age``**: (``int``) ``Opcional``. Edad de la persona. Obligatorio, únicamente, si se trata de un niño (tipo ``1``).

- **``Activity``**: (``object``) ``Requerido``. Información sobre la actividad.
    - **``FromDate``**: (``date``) ``Requerido``. Fecha de inicio de la actividad. Formato IS0 8601 (YYYY-MM-DD).
    - **``ToDate``**: (``date``) ``Requerido``. Fecha de finalización de la actividad. Formato IS0 8601 (YYYY-MM-DD).
    - **``PrePackageIds``**: (``list``) ``Requerido``. Listado de prepaquetes.
        - **``(string)``**: ``Requerido``. Identificador del prepaquete.

- **``Accomodation``**: (``object``) ``Requerido``. Información sobre los hoteles a obtener.
    - **``AccommodationIds``**: (``list``) ``Opcional``. Listado que permite obtener únicamente paquetes de un conjunto de hoteles.
        - **``(string)``**:  ``Opcional``. Identificador del hotel.
    - **``Destination``**: (``object``) ``Requerido``. Geolocalización a partir de la cual se realizará la búsqueda de hoteles. Ver [SuggestedLocation](/experthubApiDocs/es/docs/package/prePackage/).
        - **``Latitude``**: (``decimal``) ``Requerido``. Latitud de la geoposición.
        - **``Longitude``**: (``decimal``) ``Requerido``. Longitud de la geoposición.
    - **``CheckIn``**: (``date``) ``Requerido``. Fecha de entrada al alojamiento. Formato ISO 8601 (YYYY-MM-DD).
    - **``CheckOut``**: (``date``) ``Requerido``. Fecha de salida del alojamiento. Formato ISO 8601 (YYYY-MM-DD).
    - **``RoomDistribution``**: (``list``) ``Requerido``. Listado habitaciones que compondrán el paquete.
        - **``Room``**: (``list``) ``Requerido``. Información de las Personas que componen esta habitación.
            - **``(int)``**: ``Requerido``. Índice correspondiente a la posición de la persona en el listado de Personas (People).
- **``Filter``**: (``list``) ``Opcional``. Filtros para acotar la obtención de paquetes. Los distintos filtros se añaden como si de un operador ``AND`` se tratase.
    - **``AccommodationBoards``**: (``list``) ``Opcional``. Listado con los regímenes del alojamiento deseados.
        - **``(int)``**: ``Opcional``. Tipo de régimen alimenticio.

            ??? example "Posibles valores"
                --8<-- "includes/enum/accommodationBoard.md"

    - **``AccommodationCategories``**: (``list``) ``Opcional``. Listado con las categorías del alojamiento deseadas.
        - **``(int)``**: ``Opcional``. Tipo de categoría del alojamiento.

            ??? example "Posibles valores"
                --8<-- "includes/enum/accommodationCategory.md"

    - **``AccommodationRateClasses``**: (``list``) ``Opcional``. Listado de alojamientos con o sin reembolso.
        - **``(int)``**: ``Opcional``. Indica si se quiere o no con reembolso.

            ??? example "Posibles valores"
                --8<-- "includes/enum/accommodationRateClass.md"

    - **``AccommodationTypes``**: (``list``) ``Opcional``. Listado de tipos de alojamiento.
        - **``(int)``**: ``Opcional``. Indica el tipo de alojamiento.
          
            ??? example "Posibles valores"
                --8<-- "includes/enum/accommodationType.md"

    - **``Cities``**: (``list``) ``Opcional``. Listado de ciudades.
        - **``(string)``**: ``Opcional``. Nombre de la ciudad.
    - **``DistanceRanges``**: (``list``) ``Opcional``. Listado de rangos de distancia. En caso de más de un elemento, actuarán como un operador de union ``OR``.
        - **``DistanceRange``**: (``object``) ``Opcional``. Rango de distancia en metros.
            - **``Min``**: (``int``) ``Opcional``. Distancia mínima.
            - **``Max``**: (``int``) ``Opcional``. Distancia máxima.
        - **``PriceRange``**: ``Opcional``. Rango de precios del paquete. En caso de más de un elemento, actuarán como un operador de union ``OR``.
            - **``Min``**: (``int``) ``Opcional``. Precio mínimo.
            - **``Max``**: (``int``) ``Opcional``. Precio máximo.
- **``Sort``**: (``object``) ``Opcional``. Ordenación de los resultados
    - **``Criteria``**: (``int``) ``Opcional``. Tipo de ordenación.

        ??? example "Posibles valores"
            --8<-- "includes/enum/sortCriteria.md"

- **``Paging``**: (``object``) ``Opcional``. Información de la paginación.
    - **``Number``**: (``int``) ``Opcional``. Número de pagina solicitada.
    - **``Size``**: (``int``) ``Opcional``. Número de elementos por página.

### Ejemplos de peticiones

??? tip "Example: 2 rooms: "1 adult + 1 child" y "1 adult""

--8<-- "includes/examples/package/basicCatalogRequest001.md"

??? tip "Example: 1 rooms: "1 adult + 1 child" in 3* accommodation"

--8<-- "includes/examples/package/basicCatalogRequest002.md"

## Estructura de la respuesta

- **``TotalPages``** (``int``) Número total de páginas.
- **``Success``** (``boolean``) Si la petición ha podido ser procesada.
- **``AvailableFilters``** (``list``) Listado de filtros disponibles para la configuración de la/s actividad/es y alojamiento/s. Hay que tener en cuenta las restricciones anteriormente mencionadas.
    - **``AccommodationBoards``** (``list``) Listado de regímenes alimenticios.
        - **``Value``** (``int``) Tipo de régimen alimenticio.

            ??? example "Posibles valores"
                --8<-- "includes/enum/accommodationBoard.md"

        - **``Count``** (``int``) Número de resultados disponibles para este régimen alimenticio.

    - **``AccommodationCategories``** (``list``) Listado con las categorías del alojamiento deseadas.
        - **``Value``** (``int``) Categoría del alojamiento.

            ??? example "Posibles valores"
                --8<-- "includes/enum/accommodationCategory.md"

        - **``Count``** (``int``) Número de resultados disponibles para esta categoría.

    - **``AccommodationCities``** (``list``) Listado con las ciudades disponibles.
        - **``Value``** (``string``) Nombre de la ciudad.
        - **``Count``** (``int``) Número de resultados disponibles para la ciudad en cuestión.

    - **``AccommodationRateClasses``** (``list``) Listado de alojamientos con o sin reembolso.
        - **``Value``** (``int``) Indica si permite reembolso.

            ??? example "Posibles valores"
                --8<-- "includes/enum/accommodationRateClass.md"

        - **``Count``** (``int``) Número de resultados para el tipo en cuestión.

    - **``AccommodationTypes``**  (``list``) Listado de tipos de alojamiento.
        - **``Value``**  (``int``) Indica el tipo de alojamiento.

            ??? example "Posibles valores"
                --8<-- "includes/enum/accommodationType.md"

        - **``Count``** (``int``) Número de resultados para cada el tipo alojamiento.

- **``Packages``** (``list``) Listado de paquetes con base en los criterios de búsqueda: Actividad/es, Alojamiento/s y Filtros.
    - **``Package``** (``object``) Información del paquete.
        - **``Accommodation``** (``object``) Información del alojamiento.
            - **``DistanceToActivity``** (``decimal``) Distancia, en metros, desde el alojamiento hasta el punto inicial de la actividad.
            - **``MainImageUrl``** (``string``) Url de la imagen principal del alojamiento.
            - **``Name``** (``string``) Nombre del alojamiento.
            - **``Description``** (``string``) Descripción del alojamiento.
            - **``Address``** (``string``) Dirección del alojamiento.
            - **``City``** (``string``) Ciudad donde se ubica el alojamiento.
            - **``PostalCode``** (``string``) Código postal del alojamiento.
            - **``Country``** (``string``) País donde está ubicado el alojamiento.
            - **``Type``** (``string``) Tipo de alojamiento.

                ??? example "Posibles valores"
                    --8<-- "includes/enum/accommodationType.md"

            - **``Category``** (``string``) Categoría del alojamiento.

                ??? example "Posibles valores"
                    --8<-- "includes/enum/accommodationCategory.md"

        - **``PriceFrom``** (``decimal``) Precio de la combinatoria más baja para el paquete en cuestión.

