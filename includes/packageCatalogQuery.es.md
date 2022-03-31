- **``Activity``**: actividad con la que queremos el paquete.
    - **``PrePackageIds``**: identificador del prepaquete de la actividad.
    - **``FromDate``**: fecha desde la que queremos hacer uso de la actividad.
    - **``ToDate``**: fecha hasta la que queremos hacer uso la actividad.

- **``Accommodation``**: información sobre el alojamiento.
    - **``CheckIn``**: fecha de acceso al alojamiento.
    - **``CheckOut``**: fecha de salida del alojamiento.
    - **``Destination``**: coordenadas del destino, para buscar hoteles cercanos.
        - **``Latitude``**: latitud.
        - **``Longitude``**: longitud.
    - **``RoomDistribution``**: array de habitaciones.
        - **`People`**: array de personas.
            - **``Type``**: tipo de persona.

                ??? example "Posibles valores"
                    - 0: Bebé
                    - 1: Niño
                    - 2: Adulto
                    - 3: Senior
                    - 4: Genérico

            - **``Age``**: edad de la persona, obligatorio en caso de ser bebé o niño.
