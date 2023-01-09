# Catálogo de paquetes

En este método podemos obtener información sobre los paquetes disponibles.

## Método de acceso

**POST** package/catalog

## Estructura de la petición

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
                    --8<-- "includes/enum/personType.md"

            - **``Age``**: edad de la persona, obligatorio en caso de ser bebé o niño.


### Ejemplo de petición

??? tip "Example"

    --8<-- "includes/examples/package/catalogQueryExamples.md"

## Estructura de la respuesta

- **``Packages``**: listado de paquetes.
    - **``Accommodation``**: información del alojamiento.
        - **``Id``**: identificador del alojamiento.
        - **``Name``**: nombre del alojamiento.
        - **`Description`**: descripción del alojamiento.
        - **``Address``**: dirección del alojamiento.
        - **``City``**: ciudad del alojamiento.
        - **``Type``**: tipo de alojamiento.

            ??? example "Posibles valores"
                --8<-- "includes/enum/accommodationType.md"

        - **``Category``**: indica la categoría del alojamiento basándose en estrellas.

            ??? example "Posibles valores"
                --8<-- "includes/enum/accommodationCategory.md"

        - **``DistanceToActivity``**: distancia del alojamiento hasta la actividad del paquete.
        - **`MainImageUrl`**: URL a la imagen principal del alojamiento.
        - **`Flags`**: información adicional.
            - **`IncludesTickets`**: indica si incluye tickets.
            - **`Promoted`**: indica si está promocionado.

    - **``PriceFrom``**: precio desde para el paquete.

- **``AvailableFilters``**: filtros disponibles.
    - **``AccommodationBoards``**: array de tipos de pensión.
        - **``Value``**: tipo de pensión.

            ??? example "Posibles Valores"
                --8<-- "includes/enum/accommodationBoard.md"

        - **``Count``**: cantidad de alojamientos.

    - **``AccommodationCategories``**: array de categorías.
        - **``Value``**: tipo de categoría.

            ??? example "Posibles valores"
                --8<-- "includes/enum/accommodationCategory.md"

        - **``Count``**: cantidad de alojamientos.

    - **``AccommodationCities``**: array de ciudades.
        - **``Value``**: nombre de la ciudad.
        - **``Count``**: cantidad de alojamientos.

    - **``AccommodationRateClasses``**: array de tipos de tarifas.
        - **``Value``**: tipo de tarifa.

            ??? example "Posibles valores"
                --8<-- "includes/enum/accommodationRateClass.md"

        - **``Count``**: cantidad de alojamientos.

    - **``AccommodationTypes``**: array de tipos de alojamientos.
        - **``Value``**: tipo de alojamiento.

            ??? example "Posibles valores"
                --8<-- "includes/enum/accommodationType.md"

        - **``Count``**: cantidad de alojamientos.

    - **``DistanceRanges``**: array de rangos de distancias.
        - **``Value``**: rango de distancia.
            - **``Min``**: mínima distancia entre alojamiento y actividad.
            - **``Max``**: máxima distancia entre alojamiento y actividad.
        - **``Count``**: cantidad de alojamientos.

    - **``PriceRanges``**: array de rangos de precios.
        - **``Value``**: rango de precio.
            - **``Min``**: mínimo precio del alojamiento.
            - **``Max``**: máximo precio del alojamiento.
        - **``Count``**: cantidad de alojamientos.

- **``TotalPages``**: número total de páginas.
--8<-- "includes/experthubResponseBaseDocumentation.es.md"

### Ejemplos

??? tip "Example"
    --8<-- "includes/examples/package/catalogResponseExamples.md"
