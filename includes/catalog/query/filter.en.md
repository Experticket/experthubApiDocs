- **`Filter`**: (`list`) `Optional`. Filters used to narrow the result set. Different filters are combined as a logical `AND`.
    - **`AccommodationBoards`**: (`list`) `Optional`. List of desired accommodation board types.
        - **`(int)`**: `Optional`. Board type.

            ??? example "Possible values"
                --8<-- "includes/enum/accommodationBoard.en.md"

    - **`AccommodationCategories`**: (`list`) `Optional`. List of desired accommodation categories.
        - **`(int)`**: `Optional`. Accommodation category type.

            ??? example "Possible values"
                --8<-- "includes/enum/accommodationCategory.en.md"

    - **`AccommodationRateClasses`**: (`list`) `Optional`. List of refundable or non-refundable accommodations.
        - **`(int)`**: `Optional`. Indicates whether refundable rates are desired.

            ??? example "Possible values"
                --8<-- "includes/enum/accommodationRateClass.en.md"

    - **`AccommodationTypes`**: (`list`) `Optional`. List of accommodation types.
        - **`(int)`**: `Optional`. Accommodation type.

            ??? example "Possible values"
                --8<-- "includes/enum/accommodationType.en.md"

    - **`Cities`**: (`list`) `Optional`. List of cities.
        - **`(string)`**: `Optional`. City name.

    - **`PriceRange`**: `Optional`. Package price range. If more than one value is specified, they behave as a logical `OR`.
        - **`Min`**: (`int`) `Optional`. Minimum price.
        - **`Max`**: (`int`) `Optional`. Maximum price.