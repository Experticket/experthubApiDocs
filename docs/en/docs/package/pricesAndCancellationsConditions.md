# Price retrieval

This method allows us to obtain a price list for the requested package, grouping, and date combination.

The definition of the groupings (`PaxGroupings`) becomes relevant when the package contains several activities and, therefore, potentially different dates for each activity.

## Access method

**POST** /Package/PricesAndCancellationConditions

## Request structure

- **`EchoToken`**: (`string`) `Required`. Token that identifies the request sequence. See [extended catalog](fullCatalog.md#response-structure).
- **`Packages`**: (`list`) `Required`. List of packages to request.
    - **`Package`**: (`object`) `Required`. Package information.
        - **`Id`**: (`string`) `Required`. Package identifier.
        - **`PaxGroupings`**: (`list`) `Required`. List of groupings.
            - **`PaxGrouping`**: (`object`) `Required`. Grouping information.
                - **`Id`**: (`string`) `Required`. Grouping identifier.
                - **`AccessDate`**: (`date`) `Required`. Activity start date. ISO 8601 format (yyyy-MM-dd).

### Request examples

??? tip "Example"

    --8<-- "includes/examples/package/pricesAndCancellationsConditions.request.1.md"

## Response structure

- **`EchoToken`**: (`string`). Token that identifies the request sequence. See [extended catalog](fullCatalog.md#response-structure).
- **`Packages`**: (`list`). List of packages requested in the call.
    - **`Package`**: (`object`). Package information.
        - **`Id`**: (`string`). Package identifier.
        - **`Price`**: (`decimal`). Package price.
        - **`PriceMode`**: (`int`). Price type.

            ??? example "Possible values"
                --8<-- "includes/enum/priceMode.en.md"

        - **`Commission`**: (`object`). Commission information.
            - **`Type`**: (`int`). Commission type.

                ??? example "Possible values"
                    --8<-- "includes/enum/comissionType.en.md"

            - **`Value`**: (`decimal`). Commission value.

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response examples

??? tip "Example"

    --8<-- "includes/examples/package/pricesAndCancellationsConditions.response.1.md"
