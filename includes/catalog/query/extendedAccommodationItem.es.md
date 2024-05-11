
- **``AccommodationId``**: (``string``) ``Requerido``. Identificador del alojamiento
- **``CheckIn``**: (``date``) ``Requerido``. Fecha de entrada al alojamiento. Formato ISO 8601 (YYYY-MM-DD).
- **``CheckOut``**: (``date``) ``Requerido``. Fecha de salida del alojamiento. Formato ISO 8601 (YYYY-MM-DD).
- **``RoomDistribution``**: (``list``) ``Requerido``. Listado habitaciones que compondrán el paquete.
    - **``Room``**: (``list``) ``Requerido``. Información de las Personas que componen esta habitación.
        - **``(int)``**: ``Requerido``. Índice correspondiente a la posición de la persona en el listado de Personas (People).