# Catálogo extendido de paquetes

En este método podemos obtener información extendida sobre los paquetes (actividad + alojamiento) disponibles. Aquí se incluye información sobre las tarifas de las diferentes habitaciones disponibles del alojamento.

## Método de acceso

**POST** Package/FullCatalog

## Estructura de la petición
- **``People``**: (``list``) ``Requerido``. Listado de personas que componen el paquete. El orden en el cual se añaden las personas en este listado repercute, posteriormente, en el índice a usar en la propiedad ``Room``
    - **``Person``**: (``object``) ``Requerido``. Información de la persona.
        - **``Type``**: (``int``) ``Requerido``. Tipo de persona.

            ??? example "Posibles valores"
                --8<-- "includes/enum/personType.md"

        - **``Age``**: (``int``) ``Opcional``. Edad de la persona. Obligatorio, únicamente, si se trata de un niño (tipo ``1``).

- **``Activity``**: (``object``) ``Requerido``. Información sobre la actividad.
    - **``FromDate``**: (``date``) ``Requerido``. Fecha de inicio de la actividad. Formato IS0 8601 (YYYY-MM-DD).
    - **``ToDate``**: (``date``) ``Requerido``. Fecha de finalización de la actividad. Formato IS0 8601 (YYYY-MM-DD).
    - **``PrePackageIds``**: (``list``) ``Requerido``. Listado de identificadores de prepaquetes de la actividad.
        - ``(string)``: ``Requerido``. Identificador del prepaquete

- **``Accommodation``**: información sobre el alojamiento.
    - **``AccommodationId``**: (``string``) ``Requerido``. Identificador del alojamiento
    - **``CheckIn``**: (``date``) ``Requerido``. Fecha de entrada al alojamiento. Formato ISO 8601 (YYYY-MM-DD).
    - **``CheckOut``**: (``date``) ``Requerido``. Fecha de salida del alojamiento. Formato ISO 8601 (YYYY-MM-DD).
    - **``Destination``**: coordenadas del destino, para buscar alojaminetos cercanos.
        - **``Latitude``**: latitud.
        - **``Longitude``**: longitud.
    - **``RoomDistribution``**: (``list``) ``Requerido``. Listado habitaciones que compondrán el paquete.
        - **``Room``**: (``list``) ``Requerido``. Información de las Personas que componen esta habitación.
            - **``(int)``**: ``Requerido``. Índice correspondiente a la posición de la persona en el listado de Personas (People).

### Ejemplo de petición

??? tip "Example: 2 rooms: "2 adult + 1 child" y "1 adult""

    --8<-- "includes/examples/package/extendedCatalog.request.1.md"

## Estructura de la respuesta

La respuesta contiene 5 propiedades importantes:

- **``Echotoken``**: (``string``). Token necesario para poder añadir paquetes al carrito.
- **``Activities``**: (``object``). Propiedad que contiene la definición del [catálogo de actividades](../activity/catalog.md#estructura-de-la-respuesta).
- **``Accommodation``**: (``object``). Información sobre el alojamiento del paquete.
    - **``Id``**: (``string``). Identificador del alojamiento.
    - **``Name``**: (``string``). Nombre del alojamiento.
    - **``Description``**: (``string``). Descripción del alojamiento.
    - **``Address``**: (``string``). Dirección del alojamiento.
    - **``City``**: (``string``). Ciudad del alojamiento.
    - **``Type``**: (``int``). tipo de alojamiento.

        ??? example "Posibles valores"
            --8<-- "includes/enum/accommodationType.md"

    - **``Category``**: (``int``). Tipo de categoría.

        ??? example "Posibles valores"
            --8<-- "includes/enum/accommodationCategory.md"

    - **``CategoryName``**: (``string``). Nombre de la categoría.
    - **``TypeName``**: (``string``). Nombre del tipo de alojamiento.
    - **``Location``**: (``object``). Localización exacta del alojamiento.
        - **``Longitude``**: (``decimal``). Longitud de la geoposición.
        - **``Latitude``**: (``decimal``). Latitud de la geoposición.
    - **``Distances``**: (``list``). Listado de distancia a las diferentes actividades del paquete.
        - **``Distance``**: (``object``). Información de la distancia a la actividad del paquete.
            - **``ActivityProviderId``**: (``string``). Identificador del proveedor de la actividad. Ver [ProviderId en el catálogo de actividades](../activity/catalog.md#estructura-de-la-respuesta).
            - **``Distance``**: (``decimal``). Distancia entre el alojamiento y la actividad en metros.
    - **``AccommodationServices``**: array de servicios disponibles en el alojamiento.
        - **``Name``**: nombre del servicio.
        - **``IsFree``**: indica si está incluido en el precio.
    - **``AccommodationImages``**: (``list``). Listado de imágenes del alojamiento.
        - **``AccommodationImage``**: (``object``). Imagen del alojamiento
            - **``Description``**: (``string``). Descripción de la imagen.
            - **``Order``**: (``int``). Orden para ser mostradas.
            - **``Url``**: (``string``). Dirección URL de la imagen.
    - **``AccommodationRooms``**: (``list``). Listado con las distintas habitaciones del alojamiento.
        - **``AccommodationRoom``**: (``object``). Información de la habitación del alojamiento.
            - **``RoomRequestNumber``**: identificador de la distribución solicitada en función de la habitación.

                ??? info "Ejemplo"
                    --8<-- "includes/examples/package/extendedCatalog.request.2.md"

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
