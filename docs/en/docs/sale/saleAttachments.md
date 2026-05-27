# Attach documents to a sale

This method allows documents to be attached to a sale, for example disability certificates or large family/single-parent family supporting documents.

## Access method

**PUT** /Sale

## Request structure

The request Content-Type must be `multipart/form-data`, including the following fields:

- **`SaleId`**: (`string`) `Required`. Sale identifier.
- **`Attachments`**: (`list[list]`) `Required`. Array in which each element is a byte array containing the document to be attached.

??? tip "Information"
    The sale identifier is obtained in the response of the [sale confirmation](../shoppingCart/sale.md) call. That function returns a list of sales with their identifiers (`Id`). That identifier is the one that must be used in this field.

### Request example

??? tip "Examples"

    --8<-- "includes/examples/sale/saleAttachmentsRequest.request.1.md"

## Response structure

- **`Timestamp`**: (`dateTime`). Time at which the request was processed. ISO 8601 format (yyyy-MM-ddThh\:mm\:ss.fffffff).

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response example

??? tip "Examples"

    --8<-- "includes/examples/sale/saleAttachmentsRequest.response.1.md"
