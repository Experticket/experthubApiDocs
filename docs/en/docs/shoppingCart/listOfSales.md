# List of sales

This method allows us to retrieve the list of sales.

## Access method

**GET** /Sale

## Request structure

The following parameters must be passed as URL query string parameters. Available filters for retrieving the sales list are:

- **`PartnerSaleId`**: (`string`). `Optional`. Partner identifier.
- **`FromTransactionDateTime`**: (`date`). `Optional`. Initial transaction creation date. ISO 8601 format (yyyy-MM-dd).
- **`ToTransactionDateTime`**: (`date`). `Optional`. Final transaction creation date. ISO 8601 format (yyyy-MM-dd).
- **`FromAccessDateTime`**: (`date`). `Optional`. Initial access date. ISO 8601 format (yyyy-MM-dd).
- **`ToAccessDateTime`**: (`date`). `Optional`. Final access date. ISO 8601 format (yyyy-MM-dd).
- **`ClientName`**: (`string`). `Optional`. Customer name.
- **`ClientEmail`**: (`string`). `Optional`. Customer email.
- **`ClientPhone`**: (`string`). `Optional`. Customer phone number.
- **`ClientDocumentIdentifier`**: (`string`). `Optional`. Customer identity document.
- **`Page`**: (`int`). `Optional`. Page number to retrieve. Default value `1`.
- **`PageSize`**: (`int`). `Optional`. Number of results to retrieve.

### Request example

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/listOfSales.request.1.md"

## Response structure

- **`Sales`**: (`list`). List of sales.
    - **`PartnerSaleId`**: (`string`). Partner identifier.
    - **`Activities`**: (`list`). List of activities.

--8<-- "includes/sale/response/listOfSales/activity.en.md"

    - **`Accommodations`**: (`list`). List of accommodations included in the sale.

--8<-- "includes/sale/response/listOfSales/accommodation.en.md"

    - **`CombinedProducts`**: (`list`). List of combined products from the activities included in the sale.

--8<-- "includes/sale/response/listOfSales/combinedProduct.en.md"

    - **`Client`**: (`object`). Sale customer data.

--8<-- "includes/sale/response/listOfSales/client.en.md"

    - **`TotalPrice`**: (`decimal`). Total sale price.
    - **`TotalPriceWithoutVat`**: (`decimal`). Total sale price without taxes.
    - **`TotalDiscount`**: (`decimal`). Total discount applied to the sale. It only appears if a discount coupon has been applied.
    - **`InsurancePolicyAmount`**: (`decimal`). Total refund insurance price.
    - **`InsurancePolicyAmountWithoutTaxes`**: (`decimal`). Total refund insurance price without taxes.

- **`PageNumber`**: (`int`). Indicates the requested page.
- **`HasPreviousPage`**: (`boolean`). Indicates whether there is a previous page.
- **`HasNextPage`**: (`boolean`). Indicates whether there is a next page.
- **`IsFirstPage`**: (`boolean`). Indicates whether the requested page is the first page.

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response example

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/listOfSales.response.1.md"
