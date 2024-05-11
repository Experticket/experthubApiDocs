# Catálogo completo de un alojamiento

En este método solicitamos la información completo de un alojamiento. Aquí se incluye información sobre las tarifas de las diferentes habitaciones disponibles.

## Método de acceso

**POST** /Accommodation/FullCatalog

## Estructura de la petición

--8<-- "includes/catalog/query/people.es.md"

--8<-- "includes/catalog/query/fullAccommodationItem.es.md"

### Ejemplo de petición

??? tip "Ejemplo: 2 habitaciones: "1 adulto + 1 niño" y "1 adulto""

    --8<-- "includes/examples/accommodation/fullCatalog.request.1.md"


## Estructura de la respuesta

- **``Echotoken``**: (``string``). Token necesario para las siguientes peticiones: solicitar precios, añadir elementos al carro, etc.
- **``Accommodations``**: (``list``). Información sobre el alojamiento indicado en la petición.
    - **``Id``**: (``string``). Identificador del alojamiento.
    - **``Name``**: (``string``). Nombre del alojamiento.
    - **``Description``**: (``string``). Descripción del alojamiento.
    - **``Address``**: (``string``). Dirección del alojamiento.
    - **``PostalCode``**: (``string``). Dirección del alojamiento.
    - **``City``**: (``string``). Ciudad del alojamiento.
    - **``Country``**: (``string``). País del alojamiento.
    - **``Type``**: (``int``). Tipo de alojamiento.

        ??? example "Posibles valores"
            --8<-- "includes/enum/accommodationType.md"

    - **``Category``**: (``int``). Tipo de categoría.

        ??? example "Posibles valores"
            --8<-- "includes/enum/accommodationCategory.md"

    - **``Location``**: (``object``). Localización exacta del alojamiento.
        - **``Latitude``**: (``decimal``). Latitud de la geolocalización.
        - **``Longitude``**: (``decimal``). Longitud de la geolocalización.

    - **``AccommodationImages``**: (``list``). Listado de imágenes del alojamiento.
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

                    - **``Commission``**: (``object``). Información sobre la comisión.
                        - **``Type``**: (``int``). Tipo de comisión

                            ??? example "Posibles valores"
                                --8<-- "includes/enum/comissionType.md"

                        - **``Value``**: (``decimal``). Valor de la comisión.

- **``Flags``**: (``list``). Listado con información adicional.
    - **``IncludesTickets``**: (``boolean``). Indica si incluye tickets.
    - **``Promoted``**: (``boolean``). Indica si está promocionado.


--8<-- "includes/experthubResponseBaseDocumentation.es.md"