# Full catalog of accommodation packages

With this method we request the complete information about the packages (activity + accommodation) available for a specific accommodation. It includes information about the rates of the different rooms available for the accommodation.

## Access method

**POST** /Package/FullCatalog

## Request structure

--8<-- "includes/catalog/query/people.en.md"

--8<-- "includes/catalog/query/activity.en.md"

- **``Accommodation``**: (``object``) ``Required``. Accommodation information.
    --8<-- "includes/catalog/query/fullAccommodationItem.en.md"

### Request example

??? tip "Example: 2 rooms: \"1 adult + 1 child\" and \"1 adult\""

    --8<-- "includes/examples/package/fullCatalog.request.1.md"

## Response structure

- **``Echotoken``**: (``string``). Token needed for subsequent requests: request prices, add items to the cart, etc.
- **``Activities``**: (``object``). Property that contains the definition of the [activities catalog](../activity/catalog.md#response-structure). All activities available for the requested prepackage are listed here.
- **``Accommodation``**: (``object``). Information about the package accommodation indicated in the request.
    - **``Id``**: (``string``). Accommodation identifier.
    - **``Name``**: (``string``). Accommodation name.
    - **``Description``**: (``string``). Accommodation description.
    - **``Address``**: (``string``). Accommodation address.
    - **``City``**: (``string``). Accommodation city.
    - **``Type``**: (``int``). Accommodation type.

        ??? example "Possible values"
            --8<-- "includes/enum/accommodationType.md"

    - **``Category``**: (``int``). Category type.

        ??? example "Possible values"
            --8<-- "includes/enum/accommodationCategory.md"

    - **``CategoryName``**: (``string``). Category name.
    - **``TypeName``**: (``string``). Accommodation type name.
    - **``Location``**: (``object``). Exact accommodation location.
        - **``Latitude``**: (``decimal``). Geolocation latitude.
        - **``Longitude``**: (``decimal``). Geolocation longitude.
    - **``Distances``**: (``list``). List of distances to the different package activities.
        - **``Distance``**: (``object``). Information about the distance to the package activity.
            - **``ActivityProviderId``**: (``string``). Activity provider identifier. See [ProviderId in the activities catalog](../activity/catalog.md#response-structure).
            - **``Distance``**: (``decimal``). Distance between the accommodation and the activity in meters.
    - **``AccommodationServices``**: (``list``). List of services available in the accommodation.
    - **``AccommodationService``**: (``object``). Information about the service available in the accommodation.
            - **``Name``**: (``string``). Service name.
            - **``IsFree``**: (``string``). Indicates whether it is included in the price.
    - **``AccommodationImages``**: (``list``). List of accommodation images.
        - **``Description``**: (``string``). Image description.
        - **``Order``**: (``int``). Display order.
        - **``Url``**: (``string``). Image URL address.
    - **``AccommodationRooms``**: (``list``). List with the different accommodation rooms.
        - **``AccommodationRoom``**: (``object``). Accommodation room information.
            - **``RoomRequestNumber``**: (``string``). Identifier of the requested distribution according to the room.

                ??? info "Example"
                    --8<-- "includes/examples/package/fullCatalog.request.2.md"

            - **``TypeName``**: (``string``). Room type name.
            - **``AccommodationRoomRates``**: (``list``). Array list with the rates of the accommodation rooms.
                - **``AccommodationRoomRate``**: (``list``). Information about the accommodation room rate.
                    - **``Id``**: (``string``). Room identifier.
                    - **``BoardCode``**: (``int``) board type code.

                        ??? example "Possible values"
                            --8<-- "includes/enum/accommodationBoard.md"

                    - **``BoardName``**: (``string``). Board type name.
                    - **``Adults``**: (``int``). Number of adults.
                    - **``Children``**: (``int``). Number of children.
                    - **``RateClass``**: rate type.

                        ??? example "Possible values"
                            --8<-- "includes/enum/accommodationRateClass.md"

- **``Flags``**: (``list``). List with additional information.
    - **``IncludesTickets``**: (``boolean``). Indicates whether tickets are included.
    - **``Promoted``**: (``boolean``). Indicates whether it is promoted.
- **``PrePackages``**: (``list``). List of available prepackages. This value matches the prepackages requested in the call (``PrePackageIds``).
    - **``Id``**: (``string``). Prepackage identifier.
    - **``Name``**: (``string``). Prepackage name.
- **``ActivityPackages``**: (``list``). List of package activities.
    - **``ActivityPackage``**: (``object``). Package activity information.
        - **``Id``**: (``string``). Activity package identifier.
        - **``Activities``**: (``list``). List of activities included in the package.
            - **``Activities``**: (``object``). Information about the activity included in the package.
                - **``ActivityId``**: (``string``). Activity identifier.
                - **``Quantity``**: (``int``). Quantity included.
- **``Packages``**: (``list``) List of packages. This list is the union between the requested prepackages, the accommodation, and the activities.
    - **``Package``**: (``list``) Package information.
        - **``Id``**: (``string``). Package identifier.
        - **``PrePackageId``**: (``string``). Prepackage identifier.
        - **``AccommodationRateId``**: (``string``). Accommodation rate identifier.
        - **``AccommodationId``**: (``string``). Accommodation identifier.
        - **``ActivityPackageId``**: (``string``). Activity package identifier.
        - **``Price``**: (``decimal``). Package price.
        - **``CancellationPolicy``**: (``object``). Cancellation policies.
            - **``IsRefundable``**: (``boolean``). Indicates whether the package is refundable at any point.
            - **``Rules``**: (``list``). Rules that define the cancellation policies.
                - **``Rule``**: (``object``). Rule that defines this cancellation policy.
                    - **``HoursInAdvanceOfAccess``**: (``int``). Hours in advance with respect to the access date to which this rule applies.
                    - **``Percentage``**: (``decimal``). Penalty percentage with respect to the price.

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response example

??? tip "Example"
    --8<-- "includes/examples/package/fullCatalog.response.1.md"
