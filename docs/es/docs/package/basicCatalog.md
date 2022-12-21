# Catálogo básico de paquetes

En este método podemos obtener la información más básica e indispensable sobre los distintos paquetes.

## Método de acceso

**POST** package/basiccatalog

## Estructura de la petición

- **``People``**: Listado de personas que componen el paquete.
    - **``Person``**: Información de la persona
        - **``Type``**: Tipo de persona. Ver [Person.Type](#persontype).
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
        - **``(int)``**: Tipo de régimen alimenticio. Ver [AccommodationBoards](#accommodationboard).
    - **``AccommodationCategories``**: Listado con las categorías del alojamiento deseadas.
        - **``(int)``**: Tipo de categoría del alojamiento. Ver [AccommodationCategories](#accommodationcategory).
    - **``AccommodationRateClasses``**: Listado de alojamientos con o sin reembolso.
        - **``(int)``**: Indica si se quiere o no con reembolso. Ver [AccommodationRateClasses](#accommodationrateclass).
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
    - **``Criteria``**: Tipo de ordenación. Ver [Sort.Criteria](#sortcriteria).


## Tipo de datos
--8<-- "docs/es/docs/enum/personType.md"

--8<-- "docs/es/docs/enum/accommodationType.md"

--8<-- "docs/es/docs/enum/accommodationCategory.md"

--8<-- "docs/es/docs/enum/accommodationRateClass.md"

--8<-- "docs/es/docs/enum/sortcriteria.md"
