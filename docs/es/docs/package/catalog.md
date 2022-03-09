# Catálogo de paquetes

En este método podemos obtener información sobre los paquetes (actividad + hotel) disponibles.

## Método de acceso

**POST** package/catalog

## Estructura de la petición

- **``People``**: array de personas para buscar habitaciones.
    - **``Type``**: tipo de personas.

        ??? example "Posibles valores"
            - 0: Bebé
            - 1: Niño
            - 2: Adulto
            - 3: Senior
            - 4: Genérico

    - **``Age``**: edad de la persona.

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
    - **``RoomDistribution``**: array de array de número de identificador de personas que conforman cada habitación.

### Ejemplo de petición

--8<-- "includes/examples/package/catalogQueryExamples.md"

## Estructura de la respuesta

- **``TotalPages``**:
- **``Packages``**:
    - **``Accommodation``**:
        - **``Id``**:
        - **``Name``**:
        - **``Address``**:
        - **``City``**:
        - **``Type``**:
        - **``Category``**:
    - **``PriceFrom``**:
- **``Success``**:
- **``Errors``**:
    - **``ErrorMessage``**:
    - **``ErrorCode``**:

### Ejemplo de respuesta
