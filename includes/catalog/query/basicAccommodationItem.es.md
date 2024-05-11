
- **``AccommodationIds``**: (``list``) ``Opcional``. Listado que permite obtener únicamente paquetes de un conjunto de alojamientos.
    - **``(string)``**:  ``Opcional``. Identificador del alojamiento.
- **``Destination``**: (``object``) ``Requerido``. Geolocalización a partir de la cual se realizará la búsqueda de alojamientos. Ver [SuggestedLocation](/experthubApiDocs/es/docs/package/prePackage/#estructura-de-la-respuesta).
    - **``Latitude``**: (``decimal``) ``Requerido``. Latitud de la geolocalización.
    - **``Longitude``**: (``decimal``) ``Requerido``. Longitud de la geolocalización.
- **``CheckIn``**: (``date``) ``Requerido``. Fecha de entrada al alojamiento. Formato ISO 8601 (YYYY-MM-DD).
- **``CheckOut``**: (``date``) ``Requerido``. Fecha de salida del alojamiento. Formato ISO 8601 (YYYY-MM-DD).
- **``RoomDistribution``**: (``list``) ``Requerido``. Listado habitaciones que compondrán el paquete.
    - **``Room``**: (``list``) ``Requerido``. Información de las Personas que componen esta habitación.
        - **``(int)``**: ``Requerido``. Índice correspondiente a la posición de la persona en el listado de Personas (People).