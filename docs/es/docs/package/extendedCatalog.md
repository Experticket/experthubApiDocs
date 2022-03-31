# Catálogo extendido de paquetes

En este método podemos obtener información extendidas sobre los paquetes (actividad + hotel) disponibles. Aquí se incluye información sobre las tarifas de las diferentes habitaciones disponibles del hotel.

## Método de acceso

**POST** package/fullcatalog

## Estructura de la petición

--8<-- "includes/packageCatalogQuery.es.md"

### Ejemplo de petición

--8<-- "includes/examples/package/catalogQueryExamples.md"

## Estructura de la respuesta

- **``Echotoken``**: token necesario para poder añadir paquetes al carrito.
- **``Activities``**: este campo contiene la definición del [catálogo de actividades](../activity/catalog.md#estructura-de-la-respuesta).
- **``Accommodation``**: información sobre el alojamiento del paquete.
    - **``Id``**: identificador del alojamiento.
    - **``Name``**: nombre del alojamiento.
    - **``Description``**: descripción del alojamiento.
    - **``Address``**: dirección del alojamiento.
    - **``City``**: ciudad del alojamiento.
    - **``Type``**: tipo de alojamiento.

        ??? example "Posibles valores"
            - 0: Sin clasificar
            - 1: Hotel
            - 2: Hostal
            - 3: Camping
            - 4: Apartamento

    - **``Category``**: tipo de categoría.

        ??? example "Posibles valores"
            - 0: Sin clasificar
            - 1: Una estrella :star:
            - 2: Dos estrellas :star::star:
            - 3: Tres estrellas :star::star::star:
            - 4: Cuatro estrellas :star::star::star::star:
            - 5: Cinco estrellas :star::star::star::star::star:

    - **``CategoryName``**: nombre de la categoría.
    - **``TypeName``**: nombre del tipo de alojamiento.
    - **``Location``**: localización exacta del alojamiento.
        - **``Longitude``**: coordenadas longitudinales.
        - **``Latitude``**: coordenadas latitudinales.
    - **``Distances``**: array de distancia a las diferentes actividades del paquete.
        - **``ActivityProviderId``**: identificador del proveedor de la actividad.
        - **``Distance``**: distancia entre el alojamiento y la actividad.
    - **``AccommodationServices``**: array de servicios disponibles en el alojamiento.
        - **``Name``**: nombre del servicio.
        - **``IsFree``**: indica si está incluido en el precio.
    - **``AccommodationImages``**: array de imágenes del alojamiento.
        - **``Description``**: descripción de la imagen.
        - **``Order``**: orden para ser mostradas.
        - **``Url``**: dirección URL de la imagen.
    - **``AccommodationRooms``**: distintas habitaciones del alojamiento.
        - **``RoomRequestNumber``**: identificador de la distribución solicitada en función de la habitación.

            ??? info "Ejemplo"
                - Si se solicitan 3 habitaciones de 2 adultos cada una.

                    En este caso aparecerán los identificadores definidos entre 1 y 3 pero será posible seleccionar las habitaciones como se quiera. Ejemplos:

                    - 3 del tipo ``RoomRequestNumber = 1``
                    - 2 del tipo ``RoomRequestNumber = 1`` y 1 del tipo ``RoomRequestNumber = 3``
                    - 1 del tipo ``RoomRequestNumber = 1``, otra del tipo ``RoomRequestNumber = 2`` y otra del tipo ``RoomRequestNumber = 3``

                - Si se solicitan 3 habitaciones, una de 2 adultos, otra de 2 niños y otra de 1 niño y 1 adulto.

                    Será necesario seleccionar una del tipo ``RoomRequestNumber = 1``, una ``RoomRequestNumber = 2`` y otra ``RoomRequestNumber = 3``.

        - **``TypeName``**: nombre del tipo de habitación.
        - **``AccommodationRoomRates``**: array con las tarifas de las habitaciones del alojamiento.
            - **``Id``**: identificador de la habitación.
            - **``Code``**: código de la habitación.
            - **``RateId``**: identificador de la tarifa.
            - **``RateComments``**: comentarios de la tarifa.
            - **``BoardCode``**: código del tipo de pensión.

                ??? example "Posibles valores"
                    - 10: solo alojamiento
                    - 20: desayuno incluido
                    - 30: media pensión
                    - 40: pensión completa
                    - 50: todo incluido

            - **``BoardName``**: nombre de la pensión.
            - **``Adults``**: número de adultos.
            - **``Children``**: número de niños.
            - **``RateClass``**: tipo de tarifa.

                ??? example "Posibles valores"
                    - 1: No reembolsable
                    - 2: Reembolsable

            - **``Price``**: precio de la tarifa.
            - **``PriceMode``**: tipo de precio.

                ??? example "Posibles valores"
                    - 1: PVP
                    - 2: Neto

    - **``Flags``**: información adicional.
        - **``IncludesTickets``**: indica si incluye tickets.
        - **``Promoted``**: indica si está promocionado.
- **``PrePackages``**: array de prepaquetes.
    - **``Id``**: identificador del prepaquete.
    - **``Name``**: nombre del prepaquete.
- **``ActivityPackages``**: array de actividades del paquete.
    - **``Id``**: identificador del paquete de actividades
    - **``Activities``**: array de actividades incluidas en el paquete.
        - **``ActivityId``**: identificador de la actividad.
        - **``Quantity``**: cantidad que se incluye.
- **``Packages``**: array de paquetes.
    - **``Id``**: identificador del paquete.
    - **``PrePackageId``**: identificador del prepaquete.
    - **``AccommodationRateId``**: identificador de la tarifa de alojamiento.
    - **``AccommodationId``**: identificador del alojamiento.
    - **``ActivityPackageId``**: identificador del paquete de actividades.
    - **``Price``**: precio del paquete.
    - **``CancellationPolicy``**: politicas de cancelación.
        - **``IsRefundable``**: indica si el paquete es reembolsable o no en algún momento.
        - **``Rules``**: reglas que definen las politicas de cancelación.
            - **``HoursInAdvanceOfAccess``**: horas de antelación respecto a la fecha de acceso sobre el que aplica esta regla.
            - **``Percentage``**: porcentaje de penalización respecto al precio.

### Ejemplo de respuesta

--8<-- "includes/examples/package/extendedCatalogResponseExamples.md"
