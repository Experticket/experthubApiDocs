# List of cancellation requests

This method allows cancellation requests for a sale to be listed.

## Access method

**GET** /salecancellationrequest

## Request structure

- **``PartnerSaleIds``**: (``list``) ``Required``. List of partner identifiers.
- **``FromCreatedDateTime``**: (``date``).  ``Optional`` Initial transaction creation date. ISO 8601 format (YYYY-MM-DD).
- **``ToCreatedDateTime``**: (``date``).  ``Optional`` Final transaction creation date. ISO 8601 format (YYYY-MM-DD).
- **``FromUpdatedDateTime``**: (``date``).  ``Optional`` Initial access date. ISO 8601 format (YYYY-MM-DD).
- **``ToUpdatedDateTime``**: (``date``).  ``Optional`` Final access date. ISO 8601 format (YYYY-MM-DD).
- **``Page``**: (``int``).  ``Optional`` Page number to retrieve. Default value `1`.

### Request example

??? tip "Examples"

    --8<-- "includes/examples/sale/listOfSaleCancellationRequest.request.1.md"

## Response structure

- **``Timestamp``**: (``dateTime``). Time at which the request was processed. ISO 8601 format (yyyy-MM-ddThh\:mm\:ss.fffffff).
- **``Sales``**: (``list``). List of sales.
    - **``PartnerSaleId``**: (``string``). List of activities.
    - **``CancellationRequests``**: (``Object``). Economic concepts of a sale.
    - **``ExperticketName``**: (``string``). Experticket name.
    - **``CancellationRequestId``**: (``string``). Cancellation request identifier.
    - **``SaleId``**: (``Object``). Sale identifier.
    - **``PartnerSaleId``**: (``string``). Partner sale identifier.
    - **``CreatedDateTime``**: (``date``). Cancellation request date.
    - **``UpdatedDateTime``**: (``date``). Cancellation request date.
    - **``Status``**: (``string``). Cancellation status.

        ??? example "Possible values"
            --8<-- "includes/enum/cancellationRequestStatus.md"

    - **``StatusComments``**: (``string``). Cancellation request status comments.
    - **``Reason``**: (``byte``). Cancellation status.

        ??? example "Possible values"
            --8<-- "includes/enum/cancellationRequestReason.md"

    - **``ReasonComments``**: (``string``). Cancellation request status comments.
- **``PageNumber``**: (``int``). Indicates the requested page.
- **``HasPreviousPage``**: (``boolean``). Indicates whether there is a previous page before the requested one.
- **``HasNextPage``**: (``boolean``). Indicates whether there is a next page.
- **``IsFirstPage``**: (``boolean``). Indicates whether the requested page corresponds to the first page.

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response example

??? tip "Examples"
    --8<-- "includes/examples/sale/listOfSaleCancellationRequest.response.1.md"