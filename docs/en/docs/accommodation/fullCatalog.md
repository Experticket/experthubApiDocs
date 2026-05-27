# Full accommodation catalog

With this method we request the full information of an accommodation. It includes information about the rates of the different available rooms.

## Access method

**POST** /Accommodation/FullCatalog

## Request structure

--8<-- "includes/catalog/query/people.en.md"

--8<-- "includes/catalog/query/fullAccommodationItem.en.md"

### Request example

??? tip "Example: 2 rooms: \"1 adult + 1 child\" and \"1 adult\""

    --8<-- "includes/examples/accommodation/fullCatalog.request.1.md"

## Response structure

- **`Echotoken`**: (`string`). Token needed for subsequent requests such as requesting prices, adding items to the cart, etc.
- **`Accommodations`**: (`list`). Information about the accommodation specified in the request.
    - **`Id`**: (`string`). Accommodation identifier.
    - **`Name`**: (`string`). Accommodation name.
    - **`Description`**: (`string`). Accommodation description.
    - **`Address`**: (`string`). Accommodation address.
    - **`PostalCode`**: (`string`). Accommodation postal code.
    - **`City`**: (`string`). Accommodation city.
    - **`Country`**: (`string`). Accommodation country.
    - **`Type`**: (`int`). Accommodation type.

        ??? example "Possible values"
            --8<-- "includes/enum/accommodationType.en.md"

    - **`Category`**: (`int`). Category type.

        ??? example "Possible values"
            --8<-- "includes/enum/accommodationCategory.en.md"

    - **`Location`**: (`object`). Exact accommodation location.
        - **`Latitude`**: (`decimal`). Location latitude.
        - **`Longitude`**: (`decimal`). Location longitude.

    - **`AccommodationImages`**: (`list`). List of accommodation images.
        - **`Description`**: (`string`). Image description.
        - **`Order`**: (`int`). Display order.
        - **`Url`**: (`string`). Image URL.

    - **`AccommodationRooms`**: (`list`). List of different accommodation rooms.
        - **`AccommodationRoom`**: (`object`). Information about the accommodation room.
            - **`RoomRequestNumber`**: (`string`). Requested distribution identifier according to the room.

                ??? info "Example"
                    --8<-- "includes/examples/package/fullCatalog.request.2.md"

            - **`TypeName`**: (`string`). Room type name.
            - **`AccommodationRoomRates`**: (`list`). Array with the accommodation room rates.
                - **`AccommodationRoomRate`**: (`list`). Information about the room rate.
                    - **`Id`**: (`string`). Room identifier.
                    - **`BoardCode`**: (`int`). Board type code.

                        ??? example "Possible values"
                            --8<-- "includes/enum/accommodationBoard.en.md"

                    - **`BoardName`**: (`string`). Board type name.
                    - **`Adults`**: (`int`). Number of adults.
                    - **`Children`**: (`int`). Number of children.
                    - **`RateClass`**: Rate type.

                        ??? example "Possible values"
                            --8<-- "includes/enum/accommodationRateClass.en.md"

                    - **`Price`**: (`decimal`). Rate price.
                    - **`PriceMode`**: (`int`). Price type.

                        ??? example "Possible values"
                            --8<-- "includes/enum/priceMode.en.md"

                    - **`Commission`**: (`object`). Commission information.
                        - **`Type`**: (`int`). Commission type.

                            ??? example "Possible values"
                                --8<-- "includes/enum/comissionType.md"

                        - **`Value`**: (`decimal`). Commission value.

- **`Flags`**: (`list`). List with additional information.
    - **`IncludesTickets`**: (`boolean`). Indicates whether tickets are included.
    - **`Promoted`**: (`boolean`). Indicates whether it is promoted.

--8<-- "includes/experthubResponseBaseDocumentation.en.md"