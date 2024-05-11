# Extended package catalog

In this method we can obtain extended information about the packages (activity + hotel) available. Here is information on the rates of the different rooms available at the hotel.

## Access method

**POST** package/fullcatalog

## Request structure

--8<-- "includes/packageCatalogQuery.en.md"

### Request example

--8<-- "includes/examples/package/catalogQueryExamples.md"

## Response structure

- **``Echotoken``**: token needed to be able to add packages to the cart.
- **``Activities``**: this field contains the definition of the [activity catalog](../activity/catalog.md#response-structure).
- **``Accommodation``**: package accommodation information.
    - **``Id``**: accommodation identifier.
    - **``Name``**: accommodation name.
    - **``Description``**: accommodation description.
    - **``Address``**: accommodation address.
    - **``City``**: accommodation city.
    - **``Type``**: type of accommodation.

        ??? example "Possible values"
            - 0: Unclassified
            - 1: Hotel
            - 2: Hostel
            - 3: Camping
            - 4: Apartment

    - **``Category``**: category type.

        ??? example "Possible values"
            - 0: Unclassified
            - 1: One star :star:
            - 2: Two stars :star::star:
            - 3: Three stars :star::star::star:
            - 4: Four stars :star::star::star::star:
            - 5: Five stars :star::star::star::star::star:

    - **``CategoryName``**: category name.
    - **``TypeName``**: accommodation type name.
    - **``Location``**: exact location of the accommodation.
        - **``Longitude``**: longitudinal coordinates.
        - **``Latitude``**: latitudinal coordinates.
    - **``Distances``**: array of distance to the different activities of the package.
        - **``ActivityProviderId``**: identifier of the activity provider.
        - **``Distance``**: distance between accommodation and activity.
    - **``AccommodationServices``**: array of services available in the accommodation.
        - **``Name``**: service name.
        - **``IsFree``**: indicate if it is included in the price.
    - **``AccommodationImages``**: array of images of the accommodation.
        - **``Description``**: image description.
        - **``Order``**: order to be displayed.
        - **``Url``**: image url.
    - **``AccommodationRooms``**: different rooms of the accommodation.
        - **``RoomRequestNumber``**: identifier of the requested distribution according to the room.

            ??? info "Example"
                - If 3 rooms of 2 adults each are requested.

                    In this case, the identifiers defined between 1 and 3 will appear, but it will be possible to select the rooms as desired. Examples:

                    - 3 of type ``RoomRequestNumber = 1``
                    - 2 of type ``RoomRequestNumber = 1`` and 1 of type ``RoomRequestNumber = 3``
                    - 1 of type ``RoomRequestNumber = 1``, other of type ``RoomRequestNumber = 2`` and another of type ``RoomRequestNumber = 3``

                - If 3 rooms are requested, one for 2 adults, one for 2 children and one for 1 child and 1 adult.

                    It will be necessary to select one of the type ``RoomRequestNumber = 1``, one ``RoomRequestNumber = 2`` and another ``RoomRequestNumber = 3``.

        - **``TypeName``**: room type name.
        - **``AccommodationRoomRates``**: array with the room rates of the accommodation.
            - **``Id``**: room identifier.
            - **``Code``**: room code.
            - **``RateId``**: rate identifier.
            - **``RateComments``**: rate comments.
            - **``BoardCode``**: board type code.

                ??? example "Possible values"
                    - 10: accommodation only
                    - 20: bed and breakfast
                    - 30: half board
                    - 40: full board
                    - 50: all included

            - **``BoardName``**: board name.
            - **``Adults``**: number of adults.
            - **``Children``**: number of children.
            - **``RateClass``**: rate type.

                ??? example "Possible values"
                    - 1: non refundable
                    - 2: refundable

            - **``Price``**: rate price.
            - **``PriceMode``**: kind of price.

                ??? example "Possible values"
                    - 1: RRP
                    - 2: Net price

    - **``Flags``**: additional information.
        - **``IncludesTickets``**: indicates if it includes tickets.
        - **``Promoted``**: indicates if it is promoted.
- **``PrePackages``**: prepackage array.
    - **``Id``**: prepackage identifier.
    - **``Name``**: prepackage name.
- **``ActivityPackages``**: array of package activities.
    - **``Id``**: activity pack identifier
    - **``Activities``**: array of activities included in the package.
        - **``ActivityId``**: activity identifier.
        - **``Quantity``**: amount included.
- **``Packages``**: array of packages.
    - **``Id``**: package identifier.
    - **``PrePackageId``**: prepackage identifier.
    - **``AccommodationRateId``**: accommodation rate identifier.
    - **``AccommodationId``**: accommodation identifier.
    - **``ActivityPackageId``**: activity pack identifier.
    - **``Price``**: package price.
    - **``CancellationPolicy``**: cancellation policies.
        - **``IsRefundable``**: indicates whether or not the package is refundable at any point.
        - **``Rules``**: rules that define cancellation policies.
            - **``HoursInAdvanceOfAccess``**: hours in advance of the date of access to which this rule applies.
            - **``Percentage``**: percentage of penalty with respect to the price.

### Response example

--8<-- "includes/examples/package/fullCatalogResponseExamples.md"
