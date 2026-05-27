        - **`Activity`**: (`object`). Activity information.
            - **`ProductId`**: (`string`). Product identifier.
            - **`CombinedProductId`**: (`string`) `Optional`. Combined product identifier.
            - **`CombinedProductDiscriminator`**: (`byte`) `Optional`. Indicates which combined product it belongs to within the [Combined product annex](../annex/combinedProduct.en.md) array.
            - **`AccessCode`**: (`string`) `Optional`. Barcode, when applicable.
            - **`AccessDateTime`**: (`date`) `Required`. Access date. ISO 8601 format (yyyy-MM-dd).
            - **`Quantity`**: (`int`) `Required`. Product quantity.
            - **`ProductName`**: (`string`). Product name.
            - **`ProviderId`**: (`string`). Provider identifier.
            - **`ProviderName`**: (`string`). Provider name.
            - **`Price`**: (`decimal`). Sale price of the product.
            - **`PriceWithoutVat`**: (`decimal`). Sale price of the product without taxes.
            - **`PriceMode`**: (`int`). Price type:

                ??? example "Possible values"
                    --8<-- "includes/enum/priceMode.en.md"

            - **`Status`**: (`int`). Activity status.

                ??? example "Possible values"
                    --8<-- "includes/enum/activityStatus.md"

            - **`Discount`**: (`decimal`). Total discount applied to the product. It only appears if any discount coupon has been applied.
            - **`DiscountCoupons`**: (`list`). Discount coupons applied to the product. It only appears when any discount coupon has been applied.
                - **`DiscountCouponId`**: (`string`). Discount coupon identifier.
                - **`Name`**: (`string`). Discount coupon name.
                - **`Description`**: (`string`). Discount coupon description.
                - **`Discount`**: (`decimal`). Discount generated on the product.
                - **`Code`**: (`string`). Code used to apply the discount coupon.
            - **`FinancialRatios`**: (`object`). Economic concepts of a sale.
                - **`ReferenceSalePrice`**: (`object`). Reference sale price.
                    --8<-- "includes/annex/financialRatios.en.md"
                - **`Discount`**: (`object`). Commercial discount.
                    --8<-- "includes/annex/financialRatios.en.md"
                - **`Commission`**: (`object`). Partner cost.
                    --8<-- "includes/annex/financialRatios.en.md"
            - **`SalePrice`**: (`object`). Sale price.
            - **`Tickets`**: (`object`) `Optional`. List containing ticket information.
                - **`TicketId`**: (`string`) `Required`. Ticket identifier.
                - **`SessionId`**: (`string`) `Optional`. Session identifier.
                - **`SessionTime`**: (`date`) `Optional`. Session time.
                - **`AccessDateTime`**: (`date`) `Required`. Builds the suggested message to be shown regarding the access date in the access document according to `AccessDateCriteria`, `AccessDateCriteriaOpenDateSalesDocument`, `AccessDateTime`, and `AccessEndDateTime`.
                - **`AccessEndDateTime`**: (`date`) `Required`. If present, indicates the end date of ticket access validity. ISO 8601 format (yyyy-MM-dd).
                - **`SuggestedAccessDateMessage`**: (`string`). Suggested access date message.
                - **`AccessCode`**: (`string`) `Optional`. Barcode, when applicable.
                - **`TicketEnclosureId`**: (`string`). Ticket enclosure identifier.
                - **`TicketEnclosureName`**: (`string`). Ticket enclosure name.
                - **`Questions`**: (`object`) `Optional`. Ticket question information.
                    - **`TicketQuestionId`**: (`string`) `Required`. Question identifier.
                    - **`Question`**: (`string`). Question.
                    - **`StringValue`**: (`string`). Example answer of type `string`.
                    ??? info "Additional information"
                        - Depending on the question type, the answer value is returned in one property or another. For example, if the question is text type (`DataType` = 0), the `StringValue` property will be returned.
                        - Another example: if the question is date type (`DataType` = 4), the `DateTimeValue` property will be returned, and so on.
                        ??? example "Possible values"
                            --8<-- "includes/enum/examenResponseQuestions.md"

            - **`CancellationConditions`**: (`object`). Indicates the cancellation policies that apply when cancelling the sale of this product.
                - **`IsRefundable`**: (`boolean`). Indicates whether the customer can cancel free of charge at any point.
                - **`Rules`**: (`list`). Rules applied when cancelling.
                    - **`Percentage`**: (`decimal`). Penalty percentage on the ticket price.
                    - **`Amount`**: (`decimal`). Total cancellation amount.
                    - **`FromInclusiveDateTime`**: (`date`). Date from which the penalty applies, inclusive. ISO 8601 format (yyyy-MM-dd).
                    - **`ToExclusiveDateTime`**: (`date`). Date until which the penalty applies, exclusive. ISO 8601 format (yyyy-MM-dd).
                    - **`HoursInAdvanceOfAccess`**: (`int`). Number of hours in advance with respect to the access date from which the penalty amount indicated in `Amount` will be applied.