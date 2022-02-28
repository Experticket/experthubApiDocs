# Check auto assigned sessions

There may be products whose sessions cannot be chosen or it is not mandatory to choose them, in this case it is the system that assigns the sessions according to availability.

To find out if a product has auto-assigned sessions, check the **``TicketEnclosureAutoAssignSessionType``** property of the enclosure sessions node in the [catalog](catalog.md).

??? example "Possible values of TicketEnclosureAutoAssignSessionType"
    --8<-- "includes/annex/autoAssignSessionType.en.md"

Once the query is launched, the session that will be assigned when the cart is confirmed will be returned for information purposes.

!!! warning "The session obtained may not be the session assigned at the time of confirming the cart."

## Access method

**POST** /autoassignsessions

## Request data structure

- **`LanguageCode`**: defines the language in which the texts will be displayed. *ISO 639-1 Format*.
- **`Products`**: array of products for which you want to check the sessions.
    - **`ProductId`**: product identifier.
    - **`Quantity`**: product quantity.
    - **`AccessDate`**: access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **`Tickets`**: array of tickets for which we want to check auto assignment.
        - **`TicketId`**: ticket identifier.
        - **`AccessDate`**: *optional*, if indicated, it takes priority over the date indicated at the product level. *ISO 8601 format (yyyy-MM-dd)*.

### Request example

--8<-- "includes/examples/activity/autoAssignSessionQueryExamples.md"

## Response data structure

- **`Products`**: array containing the requested products.
    - **`ProductId`**: product identifier.
    - **`AccessDate`**: product access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **`HasTicketEnclosures`**: boolean indicating whether the product has enclosures.
    - **`Tickets`**: array of requested product tickets.
        - **`TicketId`**: ticket identifier.
        - **`AccessDate`**: ticket access date. *ISO 8601 format (yyyy-MM-dd)*.
        - **`TicketEnclosureId`**: enclosure identifier.
        - **`SessionId`**: assigned session identifier.
        - **`SessionTime`**: time of the assigned session in case of having been able to assign any.
        - **`SessionContentId`**: session content identifier.
        - **`SessionContentName`**: session content name.
        - **`ResultType`**: attribute indicating the result of the auto assignment.

            ??? example "Possible values"
                - 0: **Ok**. Auto assignment was successful.
                - 1: **HasNotTicketEnclosure**. The product has no enclosures, therefore it is a product without sessions.
                - 2: **TicketEnclosureSessionTypeIsNone**. The product does not have sessions in any of its enclosures.
                - 3: **TicketEnclosureDoesNotAcceptAutoAssign**. The product does not have enclosures with sessions configured as auto-assignable.
                - 4: **TicketEnclosureHasNoSessionsAvailable**. There are no sessions available for the selected product and date.

    - **`Timestamp`**: instant of time in which the response is received.
    - **`ErrorMessage`**: error message explaining why the fetching of the sessions was unsuccessful. If it was correct, the field does not appear.

### Response example

--8<-- "includes/AutoAssignSessionResultExamples.md"
