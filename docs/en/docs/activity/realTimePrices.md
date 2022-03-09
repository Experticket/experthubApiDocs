# Real time prices

Through this method we can calculate the prices of one or several products, for one or multiple dates of access.

!!! success ""
    If the product does not have the **`RequiresRealTimePrice`** field in [catalog](catalog.md) set to `#!csharp true` then there is no need to make this call.

!!! warning ""
    If the product has the **`RequiresRealTimePrice`** field of the [catalog](catalog.md) set to `#!csharp true` then we must make this call every time we want to offer to the customer that product to know its current price. In the [catalog](catalog.md) a base price is offered which can be altered (increase or discount) depending on certain factors.

!!! info "Why do we talk about price in real time?"

    The price of a product depends on the moment in which the consultation is made. There are factors such as the days remaining until the date of access or the season, which cause the price to vary.

## Access method

**POST** /realTimePrices

## Request structure

- **`ProductIds`**: array of product identifiers.
- **`AccessDates`**: array of input dates that we want to query. *ISO 8601 format (yyyy-MM-dd)**.
- **`StartDate`**: start of the input date range we want to query. Complements `AccessDates` and requires `EndDate` to be specified. *ISO 8601 format (yyyy-MM-dd)*.
- **`EndDate`**: end of the input date range we want to query. Complements `AccessDates` and requires `StartDate` to be specified. *ISO 8601 format (yyyy-MM-dd)*.
- **`CombinedProducts`**: array of combined products.
    - **`CombinedProductId`**: combined product identifier.
    - **`Products`**: array of products included in the combined product.
        - **`ProductId`**: combined product identifier.
        - **`AccessDate`**: access date. *ISO 8601 format (yyyy-MM-dd)*.

### Request examples

--8<-- "includes/examples/activity/realTimePricesQueryExamples.md"

## Response structure

- **`ProductsRealTimePrices`**: array of prices in real time.
    - **`ProductId`**: product identifier.
    - **`AccessDate`**: access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **`Price`**: price at which the product should be sold.
    - **`PriceMode`**: price kind.

        ??? example "Possible values"
            - 1: RRP
            - 2: Net price

    - **`CombinedProductId`**: combined product identifier.
    - **`CombinedProductProducts`**: array of products included in the combined product.
        - **`ProductId`**: product identifier.
        - **`AccessDate`**: access date. *ISO 8601 format (yyyy-MM-dd)*.
    --8<-- "includes/responseBaseDocumentation.es.md"

--8<-- "includes/responseBaseDocumentation.es.md"

### Response examples

--8<-- "includes/examples/activity/realTimePricesResponseExamples.md"
