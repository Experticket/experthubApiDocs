# Basic accommodation catalog

This method allows us to obtain the minimum and essential information about the different accommodations. It can be used, for example, to create an initial search page.

The result will be a list of the different available accommodations according to the search filters.

## Access method

**POST** /Accommodation/BasicCatalog

## Request structure

--8<-- "includes/catalog/query/people.en.md"

--8<-- "includes/catalog/query/basicAccommodationItem.en.md"

--8<-- "includes/catalog/query/sort.en.md"

--8<-- "includes/catalog/query/paging.en.md"

### Request examples

??? tip "Example: 2 rooms: \"1 adult + 1 child\" and \"1 adult\""

--8<-- "includes/examples/accommodation/basicCatalog.request.1.md"

??? tip "Example: 1 room: \"1 adult + 1 child\" in a 3* accommodation"

--8<-- "includes/examples/accommodation/basicCatalog.request.2.md"

## Response structure

- **`TotalPages`**: (`int`). Total number of pages.
- **`Accommodations`**: (`list`). List of accommodations.
- 
    --8<-- "includes/catalog/response/accommodationItem.en.md"

--8<-- "includes/catalog/response/availableFilters.en.md"

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response examples

??? tip "Example"
    --8<-- "includes/examples/accommodation/basicCatalog.response.1.md"