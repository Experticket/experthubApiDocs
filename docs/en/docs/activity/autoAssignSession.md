# Check auto assigned sessions

There may be products whose sessions cannot be chosen or it is not mandatory to choose them, in this case it is the system that assigns the sessions according to availability.

To find out if a product has auto-assigned sessions, check the **``TicketEnclosureAutoAssignSessionType``** property of the enclosure sessions node in the [catalog](catalog.md).

??? example "Possible values of TicketEnclosureAutoAssignSessionType"
    --8<-- "includes/annex/autoAssignSessionType.en.md"

Once the query is launched, the session that will be assigned when the cart is confirmed will be returned for information purposes.

!!! warning "The session obtained may not be the session assigned at the time of confirming the cart."

## Access method

**POST** /autoassignsessions

## Request structure

- **`LanguageCode`**: (``string``). Defines the language in which the texts will be displayed. *ISO 639-1 format*.
- **`Products`**: (``list``). Array of products for which you want to check the sessions.
    - **`ProductId`**: (``string``). Product identifier.
    - **`Quantity`**: (``int``). Product quantity.
    - **`AccessDate`**: (``date``). Access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **`Tickets`**: (``list``). Array of tickets for which we want to check auto assignment.
        - **`TicketId`**: (``string``). Ticket identifier.
        - **`AccessDate`**: (``date``) ``Optional``. If indicated, it takes priority over the date indicated at the product level. *ISO 8601 format (yyyy-MM-dd)*.

### Request example

--8<-- "includes/examples/activity/autoAssignSessionQueryExamples.md"

## Response structure

- **`Products`**: (``list``). Array containing the requested products.
    - **`ProductId`**: (``string``). Product identifier.
    - **`AccessDate`**: (``date``). Product access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **`HasTicketEnclosures`**: (``boolean``). Boolean indicating whether the product has enclosures.
    - **`Tickets`**: (``list``). Array of requested product tickets.
        - **`TicketId`**: (``string``). Ticket identifier.
        - **`AccessDate`**: (``date``). Ticket access date. *ISO 8601 format (yyyy-MM-dd)*.
        - **`TicketEnclosureId`**: (``string``). Enclosure identifier.
        - **`SessionId`**: (``string``). Assigned session identifier.
        - **`SessionTime`**: (``date``). Time of the assigned session in case one could be assigned.
        - **`SessionContentId`**: (``string``). Session content identifier.
        - **`SessionContentName`**: (``string``). Session content name.
        - **`SessionStartTimeType`**: (``int``). Numeric identifier that indicates the session access start type.
            - **`0`**: (``int``): Access at the indicated time.
            - **`1`**: (``int``): Access from the indicated time onwards.
        - **`ResultType`**: (``byte``). Attribute indicating the result of the auto assignment.

            ??? example "Possible values"
                - 0: **Ok**. Auto assignment was successful.
                - 1: **HasNotTicketEnclosure**. The product has no enclosures, therefore it is a product without sessions.
                - 2: **TicketEnclosureSessionTypeIsNone**. The product does not have sessions in any of its enclosures.
                - 3: **TicketEnclosureDoesNotAcceptAutoAssign**. The product does not have enclosures with sessions configured as auto-assignable.
                - 4: **TicketEnclosureHasNoSessionsAvailable**. There are no sessions available for the selected product and date.

--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/activity/autoAssignSessionResponseExamples.md"
