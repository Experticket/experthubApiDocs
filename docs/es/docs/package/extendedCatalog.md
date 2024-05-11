# Catálogo extendido de paquetes

En este método podemos obtener información extendida sobre los paquetes (actividad + alojamiento) disponibles. Aquí se incluye información sobre las tarifas de las diferentes habitaciones disponibles del alojamiento.

## Método de acceso

**POST** /Package/FullCatalog

## Estructura de la petición

--8<-- "includes/catalog/query/people.md"

--8<-- "includes/catalog/query/activity.md"

- **``Accommodation``**: (``object``) ``Requerido``. Información sobre el alojamiento.
    - **``AccommodationId``**: (``string``) ``Requerido``. Identificador del alojamiento
    - **``CheckIn``**: (``date``) ``Requerido``. Fecha de entrada al alojamiento. Formato ISO 8601 (YYYY-MM-DD).
    - **``CheckOut``**: (``date``) ``Requerido``. Fecha de salida del alojamiento. Formato ISO 8601 (YYYY-MM-DD).
    - **``Destination``**: Coordenadas del destino, para buscar alojamientos cercanos.
        - **``Latitude``**: latitud.
        - **``Longitude``**: longitud.
    - **``RoomDistribution``**: (``list``) ``Requerido``. Listado habitaciones que compondrán el paquete.
        - **``Room``**: (``list``) ``Requerido``. Información de las Personas que componen esta habitación.
            - **``(int)``**: ``Requerido``. Índice correspondiente a la posición de la persona en el listado de Personas (People).

### Ejemplo de petición

??? tip "Example: 2 rooms: "2 adult + 1 child" y "1 adult""

    --8<-- "includes/examples/package/extendedCatalog.request.1.md"

## Estructura de la respuesta

- **``Echotoken``**: (``string``). Token necesario para las siguientes peticiones: solicitar precios, añadir elementos al carro, etc.
- **``Activities``**: (``object``). Propiedad que contiene la definición del [catálogo de actividades](../activity/catalog.md#estructura-de-la-respuesta). Aquí están listadas todas las actividades disponibles para el prepaquete indicado.
- **``Accommodation``**: (``object``). Información sobre el alojamiento del paquete, indicado en la petición.
    - **``Id``**: (``string``). Identificador del alojamiento.
    - **``Name``**: (``string``). Nombre del alojamiento.
    - **``Description``**: (``string``). Descripción del alojamiento.
    - **``Address``**: (``string``). Dirección del alojamiento.
    - **``City``**: (``string``). Ciudad del alojamiento.
    - **``Type``**: (``int``). Tipo de alojamiento.

        ??? example "Posibles valores"
            --8<-- "includes/enum/accommodationType.md"

    - **``Category``**: (``int``). Tipo de categoría.

        ??? example "Posibles valores"
            --8<-- "includes/enum/accommodationCategory.md"

    - **``CategoryName``**: (``string``). Nombre de la categoría.
    - **``TypeName``**: (``string``). Nombre del tipo de alojamiento.
    - **``Location``**: (``object``). Localización exacta del alojamiento.
        - **``Latitude``**: (``decimal``). Latitud de la geolocalización.
        - **``Longitude``**: (``decimal``). Longitud de la geolocalización.
    - **``Distances``**: (``list``). Listado de distancia a las diferentes actividades del paquete.
        - **``Distance``**: (``object``). Información de la distancia a la actividad del paquete.
            - **``ActivityProviderId``**: (``string``). Identificador del proveedor de la actividad. Ver [ProviderId en el catálogo de actividades](../activity/catalog.md#estructura-de-la-respuesta).
            - **``Distance``**: (``decimal``). Distancia entre el alojamiento y la actividad en metros.
    - **``AccommodationServices``**: (``list``). Listado de servicios disponibles en el alojamiento.
    - **``AccommodationService``**: (``object``). Información del servicio disponible en el alojamiento.
            - **``Name``**: (``string``). Nombre del servicio.
            - **``IsFree``**: (``string``). Indica si está incluido en el precio.
    - **``AccommodationImages``**: (``list``). Listado de imágenes del alojamiento.
        - **``AccommodationImage``**: (``object``). Imagen del alojamiento
            - **``Description``**: (``string``). Descripción de la imagen.
            - **``Order``**: (``int``). Orden para ser mostradas.
            - **``Url``**: (``string``). Dirección URL de la imagen.
    - **``AccommodationRooms``**: (``list``). Listado con las distintas habitaciones del alojamiento.
        - **``AccommodationRoom``**: (``object``). Información de la habitación del alojamiento.
            - **``RoomRequestNumber``**: (``string``). Identificador de la distribución solicitada en función de la habitación.

                ??? info "Ejemplo"
                    --8<-- "includes/examples/package/extendedCatalog.request.2.md"

            - **``TypeName``**: (``string``). Nombre del tipo de habitación.
            - **``AccommodationRoomRates``**: (``list``). Listado array con las tarifas de las habitaciones del alojamiento.
                - **``AccommodationRoomRate``**: (``list``). Información de la tarifa de las habitaciones del alojamiento.
                    - **``Id``**: (``string``). Identificador de la habitación.
                    - **``BoardCode``**: (``int``) código del tipo de pensión.

                        ??? example "Posibles valores"
                            --8<-- "includes/enum/accommodationBoard.md"

                    - **``BoardName``**: (``string``). Nombre del tipo de alojamiento.
                    - **``Adults``**: (``int``). Número de adultos.
                    - **``Children``**: (``int``). Número de niños.
                    - **``RateClass``**: tipo de tarifa.

                        ??? example "Posibles valores"
                            --8<-- "includes/enum/accommodationRateClass.md"

                    - **``Price``**: (``decimal``). Precio de la tarifa.
                    - **``PriceMode``**: (``int``). Tipo de precio.

                        ??? example "Posibles valores"
                            --8<-- "includes/enum/priceMode.md"

- **``Flags``**: (``list``). Listado con información adicional.
    - **``Flag``**: (``object``). Información adicional.
        - **``IncludesTickets``**: (``boolean``). Indica si incluye tickets.
        - **``Promoted``**: (``boolean``). Indica si está promocionado.
- **``PrePackages``**: (``list``). Listado de prepaquetes disponibles. Este valor concuerda con los prepaquetes solicitados en la petición (``PrePackageIds``).
    - **``PrePackage``**: (``object``). Información del prepaquete.
        - **``Id``**: (``string``). Identificador del prepaquete.
        - **``Name``**: (``string``). Nombre del prepaquete.
- **``ActivityPackages``**: (``list``). Listado de actividades del paquete.
    - **``ActivityPackage``**: (``object``). Información de la actividad del paquete.
        - **``Id``**: (``string``). Identificador del paquete de actividades
        - **``Activities``**: (``list``). Listado de actividades incluidas en el paquete.
            - **``Activities``**: (``object``). Información de la actividad incluida en el paquete.
                - **``ActivityId``**: (``string``). Identificador de la actividad.
                - **``Quantity``**: (``int``). Cantidad que se incluye.
- **``Packages``**: (``list``) Listado de paquetes. Este listado es la unión entre los prepaquetes solicitados, el alojamiento y las actividades.
    - **``Package``**: (``list``) Información del paquete.
        - **``Id``**: (``string``). Identificador del paquete.
        - **``PrePackageId``**: (``string``). Identificador del prepaquete.
        - **``AccommodationRateId``**: (``string``). Identificador de la tarifa de alojamiento.
        - **``AccommodationId``**: (``string``). Identificador del alojamiento.
        - **``ActivityPackageId``**: (``string``). Identificador del paquete de actividades.
        - **``Price``**: (``decimal``). Precio del paquete.
        - **``CancellationPolicy``**: (``object``). Políticas de cancelación.
            - **``IsRefundable``**: (``boolean``). Indica si el paquete es reembolsable o no en algún momento.
            - **``Rules``**: (``list``). Reglas que definen las políticas de cancelación.
                - **``Rule``**: (``object``). Regla que define esta política de cancelación.
                    - **``HoursInAdvanceOfAccess``**: (``int``).  Horas de antelación respecto a la fecha de acceso sobre el que aplica esta regla.
                    - **``Percentage``**: (``decimal``). Porcentaje de penalización respecto al precio.

--8<-- "includes/experthubResponseBaseDocumentation.es.md"

### Ejemplo de respuesta

??? tip "Example"
    --8<-- "includes/examples/package/extendedCatalog.response.1.md"
