# Available dates

This method allows us to obtain date availability for each activity available within the requested package.

??? important "Implications"

    Since a package can be made up of one or more activities, there may be access restrictions that prevent all activities from being carried out on the same day. This may be due to distance between them, the time required to perform each activity, or any other restriction or incompatibility that has been configured.

    Therefore, this method must be called as many times as there are activities in the requested package.

    In the first call, we will specify the package identifier (`PackageId`) and omit the date groupings (`PaxGroupingsDates`). The response will show a list with the availability of the different activities included in the package. This way, the customer can select the access date for the **first** activity. The first activity can be any of the activities shown in the response.

    Once we have the information for the first activity and the date chosen by the customer, we will call this method again adding that first choice to `PaxGroupingsDates`. The response will show a list with the availability of the **next** activities included in the package, taking into account the **possible** restrictions introduced by the first choice and allowing the customer to choose that second activity and access date.

    We will keep repeating this last action with the remaining activities.

    === "First call example"

        --8<-- "includes/examples/package/availableDates.request.1.md"

    === "Second call example"

        --8<-- "includes/examples/package/availableDates.request.2.md"

    === "Third and subsequent call example"

        --8<-- "includes/examples/package/availableDates.request.3.md"

## Access method

**POST** /Package/AvailableDates

## Request structure

- **`EchoToken`**: (`string`). `Required`. Token that identifies the request sequence. See [extended catalog](fullCatalog.md#response-structure).
- **`PackageId`**: (`string`). `Required`. Package identifier. See property `Packages.Package.Id` in the [extended catalog](fullCatalog.md#response-structure).
- **`PaxGroupingsDates`**: (`list`). `Optional`. List of already selected groupings and dates.
    - **`PaxGroupingDates`**: (`object`). `Optional`. Grouping information.
        - **`Id`**: (`string`). `Required`. `ProductPaxGroupingId` grouping identifier.
        - **`Date`**: (`date`). `Required`. Activity access date.

### Request examples

??? tip "Example"

    --8<-- "includes/examples/package/availableDates.request.3.md"

## Response structure

- **`PaxGroupingsDates`**: (`list`). List of groupings.
    - **`PaxGroupingDates`**: (`object`). Grouping information.
        - **`Id`**: (`string`). Grouping identifier (`PaxGroupingId`).
        - **`Dates`**: (`list`). List of available dates.
            - **`(date)`**: Available date. ISO 8601 format (yyyy-MM-dd).

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response examples

??? tip "Example"

    --8<-- "includes/examples/package/availableDates.response.1.md"
