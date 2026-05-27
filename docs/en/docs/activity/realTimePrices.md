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

- **`ProductIds`**: (``list``). Array of product identifiers.
    - **``(string)``**: Product identifier.
- **`AccessDates`**: (``string``). Array of access dates we want to query. *ISO 8601 format (yyyy-MM-dd)*.
    - **``(date)``**: Dates to query.
- **`StartDate`**: (``date``). Start of the access date range we want to query. Complements `AccessDates` and requires `EndDate` to be specified. *ISO 8601 format (yyyy-MM-dd)*.
- **`EndDate`**: (``date``). End of the access date range we want to query. Complements `AccessDates` and requires `StartDate` to be specified. *ISO 8601 format (yyyy-MM-dd)*.
- **`CombinedProducts`**: (``list``). Array of combined products.
    - **`CombinedProductId`**: (``string``). Combined product identifier.
    - **`Products`**: (``list``). Array of products included in the combined product.
        - **`ProductId`**: (``string``). Combined product identifier.
        - **`AccessDate`**: (``date``). Access date. *ISO 8601 format (yyyy-MM-dd)*.

### Request examples

--8<-- "includes/examples/activity/realTimePricesQueryExamples.md"

## Response structure

- **`ProductsRealTimePrices`**: (``list``). Array of real-time prices.
    - **`ProductId`**: (``string``). Product identifier.
    - **`AccessDate`**: (``date``). Access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **`Price`**: (``decimal``). Price at which the product should be sold.
    - **`PriceMode`**: (``byte``). Price type.

        ??? example "Possible values"
            - 1: Retail price
            - 2: Net price

    - **`CombinedProductId`**: (``string``). Combined product identifier.
    - **`CombinedProductProducts`**: (``string``). Array of products included in the combined product.
        - **`ProductId`**: (``string``). Product identifier.
        - **`AccessDate`**: (``date``). Access date. *ISO 8601 format (yyyy-MM-dd)*.
    --8<-- "includes/responseBaseDocumentation.en.md"

--8<-- "includes/responseBaseDocumentation.en.md"

### Response examples

--8<-- "includes/examples/activity/realTimePricesResponseExamples.md"
