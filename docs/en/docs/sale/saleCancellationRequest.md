# Cancellation request

This method allows a cancellation request to be created for a sale.

## Access method

**POST** /salecancellationrequest

## Request structure

- **``PartnerSaleId``**: (``string``) ``Required``. Partner identifier.
- **``Reason``**: (``byte``) ``Optional``. Reasons for requesting the cancellation:

    ??? example "Possible values"
        --8<-- "includes/enum/cancellationRequestReason.md"

- **``ReasonComments``**: (``string``). ``Optional``. Comments on the transaction cancellation request.

### Request example

??? tip "Examples"

    --8<-- "includes/examples/sale/createSaleCancellationRequest.request.1.md"

## Response structure

- **``Timestamp``**: (``dateTime``). Time at which the request was processed. ISO 8601 format (yyyy-MM-ddThh\:mm\:ss.fffffff).

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response example

??? tip "Examples"
    --8<-- "includes/examples/sale/createSaleCancellationRequest.response.1.md"