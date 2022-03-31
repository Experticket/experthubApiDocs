# Catálogo de paquetes

En este método podemos obtener información sobre los paquetes disponibles.

## Método de acceso

**POST** package/catalog

## Estructura de la petición

--8<-- "includes/packageCatalogQuery.es.md"

### Ejemplo de petición

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
                - 0: Sin clasificar
                - 1: Hotel
                - 2: Hostal
                - 3: Camping
                - 4: Apartamento

        - **``Category``**: indica la categoría del alojamiento en base a estrellas.

            ??? example "Posibles valores"
                - 0: Sin clasificar
                - 1: Una estrella :star:
                - 2: Dos entrellas :star::star:
                - 3: Tres estrellas :star::star::star:
                - 4: Cuatro estrellas :star::star::star::star:
                - 5: Cinco estrellas :star::star::star::star::star:

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
                - 10: Solo alojamiento
                - 20: Desayuno incluido
                - 30: Media pensión
                - 40: Pensión completa
                - 50: Todo incluido

        - **``Count``**: cantidad de alojamientos.

    - **``AccommodationCategories``**: array de categorías.
        - **``Value``**: tipo de categoría.

            ??? example "Posibles valores"
                - 0: Sin clasificar
                - 1: Una estrella :star:
                - 2: Dos entrellas :star::star:
                - 3: Tres estrellas :star::star::star:
                - 4: Cuatro estrellas :star::star::star::star:
                - 5: Cinco estrellas :star::star::star::star::star:

        - **``Count``**: cantidad de alojamientos.

    - **``AccommodationCities``**: array de ciudades.
        - **``Value``**: nombre de la ciudad.
        - **``Count``**: cantidad de alojamientos.

    - **``AccommodationRateClasses``**: array de tipos de tarifas.
        - **``Value``**: tipo de tarifa.

            ??? example "Posibles valores"
                - 1: No reembolsable
                - 2: Reembolsable

        - **``Count``**: cantidad de alojamientos.

    - **``AccommodationTypes``**: array de tipos de alojamientos.
        - **``Value``**: tipo de alojamiento.

            ??? example "Posibles valores"
                - 0: Sin clasificar
                - 1: Hotel
                - 2: Hostal
                - 3: Camping
                - 4: Apartamento

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

### Ejemplo de respuesta

--8<-- "includes/examples/package/catalogResponseExamples.md"
