# Combined product information

- **`CombinedProductId`**: (`string`). Combined product identifier.
- **`CombinedProductDiscriminator`**: (`string`). Relationship between the product (array of `Products`) and the combined product.
- **`Price`**: (`decimal`). Price of each combined product.
- **`PriceWithoutVat`**: (`decimal`). Price of each combined product without taxes.
- **`CancellationConditions`**: (`object`). Indicates the cancellation policies that apply when cancelling the sale of this product.
    - **`IsRefundable`**: (`boolean`). Indicates whether the customer can cancel free of charge at any point.
    - **`Rules`**: (`list`). Rules applied when cancelling.
        - **`Percentage`**: (`decimal`). Penalty percentage on the ticket price.
        - **`Amount`**: (`decimal`). Total cancellation amount.
        - **`FromInclusiveDateTime`**: (`date`). Date from which the penalty applies, inclusive. ISO 8601 format (yyyy-MM-dd).
        - **`ToExclusiveDateTime`**: (`date`). Date until which the penalty applies, exclusive. ISO 8601 format (yyyy-MM-dd).
        - **`HoursInAdvanceOfAccess`**: (`int`). Number of hours in advance with respect to the access date from which the penalty amount indicated in `Amount` will be applied.
