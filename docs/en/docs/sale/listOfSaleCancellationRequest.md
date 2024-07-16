# List of Cancellation Requests

This method allows creating a cancellation request for a sale.

## Access Method

**GET** /salecancellationrequest

## Request Structure

- **`PartnerSaleIds`**: (`list`) **Required**. List of partner identifiers.
- **`FromCreatedDateTime`**: (`date`). **Optional** Initial creation date of the transaction. ISO 8601 format (YYYY-MM-DD).
- **`ToCreatedDateTime`**: (`date`). **Optional** Final creation date of the transaction. ISO 8601 format (YYYY-MM-DD).
- **`FromUpdatedDateTime`**: (`date`). **Optional** Initial access date. ISO 8601 format (YYYY-MM-DD).
- **`ToUpdatedDateTime`**: (`date`). **Optional** Final access date. ISO 8601 format (YYYY-MM-DD).
- **`Page`**: (`int`). **Optional** Page number to retrieve. Default value `1`.

### Example Call

??? tip "Examples"

    --8<-- "includes/examples/sale/listOfSaleCancellationRequest.request.1.md"

## Response Structure

- **`Timestamp`**: (`dateTime`). The time when the request was processed. ISO 8601 format (yyyy-MM-ddThh:mm:ss.fffffff).
- **`Sales`**: (`list`). List of sales.
  - **`PartnerSaleId`**: (`string`). List of activities.
  - **`CancellationRequests`**: (`object`). Economic concepts of a sale.
    - **`ExperticketName`**: (`string`). Name of Experticket.
      - **`CancellationRequestId`**: (`string`). Identifier of the cancellation request.
      - **`SaleId`**: (`object`). Identifier of the sale.
      - **`PartnerSaleId`**: (`string`). Identifier of the partner's sale.
      - **`CreatedDateTime`**: (`date`). Date of the cancellation request.
      - **`UpdatedDateTime`**: (`date`). Date of the cancellation request update.
        - **`Status`**: (`string`). Status of the cancellation.

          ??? example "Possible values"
          --8<-- "includes/enum/cancellationRequestStatus.md"

      - **`StatusComments`**: (`string`). Comments on the status of the cancellation request.
        - **`Reason`**: (`byte`). Reason for the cancellation.

          ??? example "Possible values"
          --8<-- "includes/enum/cancellationRequestReason.md"

      - **`ReasonComments`**: (`string`). Comments on the reason for the cancellation request.
- **`PageNumber`**: (`int`). Indicates the requested page number.
- **`HasPreviousPage`**: (`boolean`). Indicates if there is a previous page.
- **`HasNextPage`**: (`boolean`). Indicates if there is a next page.
- **`IsFirstPage`**: (`boolean`). Indicates if the requested page is the first page.

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Example Response

??? tip "Examples"

    --8<-- "includes/examples/sale/listOfSaleCancellationRequest.response.1.md"