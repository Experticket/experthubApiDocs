# Catálogo básico de paquetes

En este método podemos obtener la información más básica e indispensable sobre los distintos paquetes.

## Método de acceso

**POST** Package/BasicCatalog

## Estructura de la petición

- **``People``**: (list) Listado de personas que componen el paquete.
    - **``Person``**: (object) Información de la persona
        - **``Type``**: (int) Tipo de persona.

            ??? example "Posibles valores"
                --8<-- "docs/es/docs/enum/personType.md"

        - **``Age``**: (int) En caso de ser niño, edad del mismo.

- **``Activity``**: (object) Información sobre la actividad.
    - **``FromDate``**: (date) Fecha de inicio de la actividad. Formato IS0 8601 (YYYY-MM-DD).
    - **``ToDate``**: (date) Fecha de finalización de la actividad. Formato IS0 8601 (YYYY-MM-DD).
    - **``PrePackageIds``**: (list) Listado de prepaquetes.
        - **``(string)``**: Identificador del prepaquete.

- **``Accomodation``**: (object) Información sobre los hoteles a obtener.
    - **``AccommodationIds``**: (list) Listado que permite obtener únicamente paquetes de un conjunto de hoteles.
        - **``(string)``**: Identificador del hotel.
    - **``Destination``**: (object) Geolocalización a partir de la cual se realizará la búsqueda de hoteles. Ver [SuggestedLocation](/experthubApiDocs/es/docs/package/prePackage/).
        - **``Latitude``**: Latitud de la geoposición.
        - **``Longitude``**: Longitud de la geoposición.
    - **``CheckIn``**: (date) Fecha de entrada al alojamiento. Formato ISO 8601 (YYYY-MM-DD).
    - **``CheckOut``**: (date) Fecha de salida del alojamiento. Formato ISO 8601 (YYYY-MM-DD).
    - **``RoomDistribution``**: (list) Listado habitaciones que compondrán el paquete.
        - **``Room``**: (list) Información de las Personas que componen esta habitación.
            - **``(int)``**: Índice correspondiente a la posición de la persona en el listado de Personas (People).
- **``Filter``**: (list) Filtros para acotar la obtención de paquetes. Los distintos filtros se añaden como si de un operador ``AND`` se tratase.
    - **``AccommodationBoards``**: (list) Listado con los regímenes del alojamiento deseados.
        - **``(int)``**: Tipo de régimen alimenticio.

            ??? example "Posibles valores"
                --8<-- "docs/es/docs/enum/accommodationBoard.md"

    - **``AccommodationCategories``**: (list) Listado con las categorías del alojamiento deseadas.
        - **``(int)``**: Tipo de categoría del alojamiento. Ver [AccommodationCategory](#accommodationcategory).
    - **``AccommodationRateClasses``**: (list) Listado de alojamientos con o sin reembolso.
        - **``(int)``**: Indica si se quiere o no con reembolso. Ver [AccommodationRateClass](#accommodationrateclass).
    - **``AccommodationTypes``**: (list) Listado de tipos de alojamiento.
        - **``(int)``**: Indica el tipo de alojamiento.
          
            ??? example "Posibles valores"
                --8<-- "docs/es/docs/enum/accommodationType.md"

    - **``Cities``**: (list) Listado de ciudades.
        - **``(string)``**: Nombre de la ciudad.
    - **``DistanceRanges``**: (list) Listado de rangos de distancia. En caso de más de un elemento, actuarán como un operador de union ``OR``.
        - **``DistanceRange``**: (object)Rango de distancia en metros.
            - **``Min``**: (int) Distancia mínima.
            - **``Max``**: (int) Distancia máxima.
        - **``PriceRange``**: Rango de precios del paquete. En caso de más de un elemento, actuarán como un operador de union ``OR``.
            - **``Min``**: (int) Precio mínimo.
            - **``Max``**: (int) Precio máximo.
- **``Sort``**: (object) Ordenación de los resultados
    - **``Criteria``**: (int) Tipo de ordenación. Ver [Sort.Criteria](#sortcriteria).

### Ejemplos de peticiones

??? tip "Example: 2 rooms: "1 adult + 1 child" y "1 adult""

--8<-- "includes/examples/package/basicCatalogRequest001.md"

??? tip "Example: 1 rooms: "1 adult + 1 child" in 3* accommodation"

--8<-- "includes/examples/package/basicCatalogRequest002.md"

## Estructura de la respuesta

- **``TotalPages``** (int) Número total de páginas.
- **``Success``** (boolean) Estado de la respuesta.
- **``AvailableFilters``** (list) Listado de filtros disponibles para la configuración de actividad y alojamiento. Hay que tener en cuenta que, los resultados, reflejan el número de alojamientos posibles a empaquetar y no el número de paquetes resultantes.
    - **``AccommodationBoards``** (list) Listado de regímenes alimenticios.
        - **``Value``** (int) Tipo de régimen alimenticio.

            ??? example "Posibles valores"
                --8<-- "docs/es/docs/enum/accommodationBoard.md"

        - **``Count``** (int) Número de resultados disponibles para este régimen alimenticio.
    - **``AccommodationCategories``** (list) Listado con las categorías del alojamiento deseadas.
        - **``Value``** (int) Categoría del alojamiento. Ver [AccommodationCategory](#accommodationcategory).
        - **``Count``** (int) Número de resultados disponibles para esta categoría.
    - **``AccommodationCities``** (list) Listado con las ciudades disponibles.
        - **``Value``** (string) Nombre de la ciudad.
        - **``Count``** (int) Número de resultados disponibles la ciudad en cuestión.
    - **``AccommodationRateClasses``** (list) Listado de alojamientos con o sin reembolso.
        - **``Value``** (int) Indica si permite reembolso. Ver [AccommodationRateClass](#accommodationrateclass).
        - **``Count``** (int) Número de resultados para cada reembolsos y no reembolsos.
    - **``AccommodationTypes``**  (list) Listado de tipos de alojamiento.
        - **``Value``**  (int) Indica el tipo de alojamiento. Ver [Accomodation Type](#accomodation-types)
        - **``Count``** (int) Número de resultados para cada el tipo alojamiento.
- **``Packages``** (list) Listado de paquetes con base en los criterios de búsqueda: Actividad, Alojamiento y Filtros.
    - **``Package``** (object) Información del paquete.
        - **``Accommodation``** (object) Información del alojamiento.
            - **``DistanceToActivity``** (decimal) Distancia, en metros, desde el alojamiento hasta el punto inicial de la actividad.
            - **``MainImageUrl``** (string) Url de la imagen principal del alojamiento.
            - **``Name``** (string) Nombre del alojamiento.
            - **``Description``** (string) Descripción del alojamiento.
            - **``Address``** (string) Dirección del alojamiento.
            - **``City``** (string) Ciudad donde se ubica el alojamiento.
            - **``PostalCode``** (string) Código postal del alojamiento.
            - **``Country``** (string) País donde está ubicado el alojamiento.
            - **``Type``** (string) Tipo de alojamiento.

                ??? example "Posibles valores"
                    --8<-- "docs/es/docs/enum/accommodationType.md"

            - **``Category``** (string) Categoría del alojamiento. Ver [AccommodationCategory](#accommodationcategory).
        - **``PriceFrom``** (decimal) Precio de la combinatoria más baja.

## Tipo de datos

--8<-- "docs/es/docs/enum/accommodationCategory.md"

--8<-- "docs/es/docs/enum/accommodationRateClass.md"

--8<-- "docs/es/docs/enum/sortCriteria.md"
