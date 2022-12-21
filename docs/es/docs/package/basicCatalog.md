# Catálogo básico de paquetes

En este método podemos obtener la información más básica e indispensable sobre los distintos paquetes.

## Método de acceso

**POST** package/basiccatalog

## Estructura de la petición

- **``People``**: Listado de personas que componen el paquete.
    - **``Person``**: Información de la persona
        - **``Type``**: Tipo de persona. Ver [People.Type](/experthubApiDocs/es/docs/struct/).
        - **``Age``**: En caso de ser niño, edad del mismo.

- **``Activity``**: Información sobre la actividad.
- **``FromDate``**: Fecha de inicio de la actividad. Formato IS0 8601 (YYYY-MM-DD).
    - **``ToDate``**: Fecha de finalización de la actividad. Formato IS0 8601 (YYYY-MM-DD).
    - **``PrePackageIds``**: Listado de prepaquetes.
        - **``(string)``**: Identificador del prepaquete.

- **``Accomodation``**: Información sobre los hoteles a obtener.
    - **``AccommodationIds``**: Listado que permite obtener únicamente paquetes de un conjunto de hoteles.
        - **``(string)``**: Identificador del hotel.
    - **``Destination``**: Geolocalización a partir de la cual se realizará la búsqueda de hoteles. Ver [SuggestedLocation](/experthubApiDocs/es/docs/package/prePackage/).
        - **``Latitude``**: Latitud de la geoposición.
            - **``Longitude``**: Longitud de la geoposición.
    - **``CheckIn``**: Fecha de entrada al alojamiento. Formato ISO 8601 (YYYY-MM-DD).
    - **``CheckOut``**: Fecha de salida del alojamiento. Formato ISO 8601 (YYYY-MM-DD).
    - **``RoomDistribution``**: Listado con la distribución de habitaciones.
        - **``Room``**: Información de las Personas que componen esta habitación.
            - **``int``**: Índice correspondiente a la posición de la persona en el listado de Personas (People).
- **``Filter``**: Filtros para acotar la obtención de paquetes. Los distintos filtros se añaden como de un operador ``AND`` se tratara.
    - **``AccommodationBoards``**: Listado con los regímenes del alojamiento deseados.
        - **``(int)``**: Tipo de régimen alimenticio. Ver [AccommodationBoards](/experthubApiDocs/es/docs/struct/).
    - **``AccommodationCategories``**: Listado con las categorías del alojamiento deseadas.
        - **``(int)``**: Tipo de categoría del alojamiento. Ver [AccommodationCategories](/experthubApiDocs/es/docs/struct/).
    - **``AccommodationRateClasses``**: Listado de alojamientos con o sin reembolso.
        - **``(int)``**: Indica si se quiere o no con reembolso. Ver [AccommodationRateClasses](/experthubApiDocs/es/docs/struct/).
    - **``AccommodationTypes``**: Listado de tipos de alojamiento.
        - **``(int)``**: Indica el tipo de alojamiento. [Ver Accomodation Types](#accomodation-types)
    - **``Cities``**: Listado de ciudades.
        - **``(string)``**: Nombre de la ciudad.
    - **``DistanceRanges``**: Listado de rangos de distancia.
        - **``DistanceRange``**: Rango de distancia en metros.
            - **``Min``**: Distancia mínima.
            - **``Max``**: Distancia máxima.
        - **``PriceRange``**: Rango de precios del paquete.
            - **``Min``**: Precio mínimo.
            - **``Max``**: Precio máximo.
- **``Sort``**: Ordenación de los resultados
    - **``Criteria``**: Tipo de ordenación. Ver [Sort.Criteria](/experthubApiDocs/es/docs/struct/).


## Tipo de datos
--8<-- "docs/es/docs/enum/accommodationType.md"