- **`People`**: (`list`) `Required`. List of people included in the package. The order in which people are added to this list later determines the index to use in the `Room` property.
    - **`Person`**: (`object`) `Required`. Person information.
        - **`Type`**: (`int`) `Required`. Person type.

            ??? example "Possible values"
                --8<-- "includes/enum/personType.en.md"

        - **`Age`**: (`int`) `Optional`. Person age. Required only if the person is a child or a baby (types `1` and `2`).