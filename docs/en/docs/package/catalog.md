# Package catalog

In this method we can obtain information about the available packages.

## Access method

**POST** package/catalog

## Request structure

--8<-- "includes/packageCatalogQuery.en.md"

### Request Example

--8<-- "includes/examples/package/catalogQueryExamples.md"

## Response structure

- **``Packages``**: list of packages.
    - **``Accommodation``**: accommodation information.
        - **``Id``**: accommodation identifier.
        - **``Name``**: accommodation name.
        - **`Description`**: accommodation description.
        - **``Address``**: accommodation address.
        - **``City``**: accommodation city.
        - **``Type``**: type of accommodation.

            ??? example "Possible values"
                - 0: Unclassified
                - 1: Hotel
                - 2: Hostel
                - 3: Camping
                - 4: Apartment

        - **``Category``**: indicates the category of accommodation based on stars.

            ??? example "Possible values"
                - 0: Unclassified
                - 1: One star :star:
                - 2: Two stars :star::star:
                - 3: Three stars :star::star::star:
                - 4: Four stars :star::star::star::star:
                - 5: Five stars :star::star::star::star::star:

        - **``DistanceToActivity``**: distance from accommodation to package activity.
        - **`MainImageUrl`**: URL to the main image of the accommodation.
        - **`Flags`**: additional information.
            - **`IncludesTickets`**: indicates if it includes tickets.
            - **`Promoted`**: indicates if it is promoted.

    - **``PriceFrom``**: price from for the package.

- **``AvailableFilters``**: available filters.
    - **``AccommodationBoards``**: array of boards.
        - **``Value``**: board type.

            ??? example "Possible values"
                - 10: Accommodation only
                - 20: Breakfast included
                - 30: Half pension
                - 40: Full board
                - 50: All included

        - **``Count``**: number of accommodations.

    - **``AccommodationCategories``**: array of categories.
        - **``Value``**: category type.

            ??? example "Possible values"
                - 0: Unclassified
                - 1: One star :star:
                - 2: Two stars :star::star:
                - 3: Three stars :star::star::star:
                - 4: Four stars :star::star::star::star:
                - 5: Five stars :star::star::star::star::star:

        - **``Count``**: number of accommodations.

    - **``AccommodationCities``**: array of cities.
        - **``Value``**: city ​​name.
        - **``Count``**: number of accommodations.

    - **``AccommodationRateClasses``**: array of rate types.
        - **``Value``**: rate type.

            ??? example "Possible values"
                - 1: Non refundable
                - 2: Refundable

        - **``Count``**: number of accommodations.

    - **``AccommodationTypes``**: array of accommodation types.
        - **``Value``**: type of accommodation.

            ??? example "Possible values"
                - 0: Unclassified
                - 1: Hotel
                - 2: Hostel
                - 3: Camping
                - 4: Apartment

        - **``Count``**: number of accommodations.

    - **``DistanceRanges``**: array of distance ranges.
        - **``Value``**: distance range.
            - **``Min``**: minimum distance between accommodation and activity.
            - **``Max``**: maximum distance between accommodation and activity.
        - **``Count``**: number of accommodations.

    - **``PriceRanges``**: array of price ranges.
        - **``Value``**: price range.
            - **``Min``**: minimum accommodation price.
            - **``Max``**: maximum accommodation price.
        - **``Count``**: number of accommodations.

- **``TotalPages``**: total number of pages.
--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/package/catalogResponseExamples.md"
