# Catálogo básico de paquetes

En este método podemos obtener la información más básica e indispensable sobre los distintos paquetes.

## Método de acceso

**POST** package/basiccatalog

## Estructura de la petición

--8<-- "docs/es/docs/package/basicCatalog/request.md"

- **``People``**: Listado de personas que componen el paquete.
    - **``Person``**: Información de la persona.
        - **``Type``**: Tipo de persona. 1: niños, 2: adultos.
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
- **``Filter``**: Filtros para acotar la obtención de paquetes.
    - **``Filter``**: Filtros para acotar la obtención de paquetes.
