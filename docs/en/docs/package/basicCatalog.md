# Basic package catalog

This method allows us to obtain the minimum and essential information about the different packages. It can be used, for example, to create an initial search page.

The result will be a matrix of the different activities (`PrePackageIds`) and the accommodations available for each of those activities.

Activities may have no accommodation restrictions, one accommodation restriction, or several accommodation restrictions configured internally, such as only being allowed to be packaged with a specific accommodation or a maximum distance restriction to the venue. These restrictions can cause accommodations not to appear in the package result list (`Packages`) even if there are accommodations available in the selected area or radius.

## Access method

**POST** /Package/BasicCatalog

## Request structure

--8<-- "includes/catalog/query/people.en.md"

--8<-- "includes/catalog/query/activity.en.md"

- **`Accomodation`**: (`object`) `Required`. Information about the accommodations to retrieve.
    --8<-- "includes/catalog/query/basicAccommodationItem.en.md"

--8<-- "includes/catalog/query/filter.en.md"

    - **`DistanceRanges`**: (`list`) `Optional`. List of distance ranges with respect to the activity. If more than one value is specified, they behave as a logical `OR`.
        - **`DistanceRange`**: (`object`) `Optional`. Distance range from the activity in meters.
            - **`Min`**: (`int`) `Optional`. Minimum distance.
            - **`Max`**: (`int`) `Optional`. Maximum distance.

--8<-- "includes/catalog/query/sort.en.md"

--8<-- "includes/catalog/query/paging.en.md"

### Request examples

??? tip "Example: 2 rooms: \"1 adult + 1 child\" and \"1 adult\""

--8<-- "includes/examples/package/basicCatalog.request.1.md"

??? tip "Example: 1 room: \"1 adult + 1 child\" in a 3* accommodation"

--8<-- "includes/examples/package/basicCatalog.request.2.md"

## Response structure

- **`TotalPages`**: (`int`). Total number of pages.
- **`Packages`**: (`list`). List of packages based on the search criteria: Activity/Activities, Accommodation(s), and Filters.
    - **`Package`**: (`object`). Package information.
        - **`Accommodation`**: (`object`). Accommodation information.

            --8<-- "includes/catalog/response/accommodationItem.en.md"

            - **`DistanceToActivity`**: (`decimal`). Distance, in meters, from the accommodation to the starting point of the activity.

        - **`PriceFrom`**: (`decimal`). Lowest combination price available for the package.

--8<-- "includes/catalog/response/availableFilters.en.md"

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response examples

??? tip "Example"
    --8<-- "includes/examples/package/basicCatalog.response.1.md"
