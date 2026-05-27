# Reserve products

This method allows the products added to the shopping cart to be reserved for a period of time.

Once the reservation has been confirmed, it is no longer possible to add more products to the cart.

## Access method

**POST** /ShoppingCart/Confirm

## Request structure

- **`ShoppingCartId`**: (`string`) `Required`. Cart identifier.

### Request examples

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/confirm.request.1.md"

## Response structure

- **`ExpirationDateTime`**: (`dateTime`). Indicates when the reservation will expire. ISO 8601 format (yyyy-MM-ddThh\:mm\:ss.d).
- **`Activities`**: (`object`). Information about the added activity.
    - **`Products`**: (`list`). List of added products.
        - **`ProductId`**: (`string`). Identifier of the added product.
        - **`CombinedProductId`**: (`string`). Identifier of the added combined product.
        - **`ProductName`**: (`string`). Name of the added product.
        - **`AccessDateTime`**: (`dateTime`). Access date and time. ISO 8601 format (yyyy-MM-ddThh\:mm\:ss.d).
        - **`Price`**: (`decimal`). Rate price.
        - **`PriceMode`**: (`int`). Price type.

            ??? example "Possible values"
                --8<-- "includes/enum/priceMode.en.md"

        - **`Success`**: (`boolean`). Indicates whether the reservation was made successfully.
        - **`Tickets`**: (`list`). List of tickets that make up this product.
            - **`Ticket`**: (`object`). Ticket information.
                - **`TicketId`**: (`string`). Ticket identifier.
        - **`CancellationPolicy`**: (`object`). Indicates the cancellation policies that apply when cancelling this product.
            - **`IsRefundable`**: (`boolean`). Indicates whether free cancellation is available at any point.
            - **`Rules`**: (`list`). List of rules applied when cancelling.
                - **`Rule`**: Information about the rule to apply.
                    - **`HoursInAdvanceOfAccess`**: (`int`). Number of hours in advance with respect to the access date from which the penalty indicated in `Percentage` will be applied.
                    - **`Percentage`**: (`decimal`). Penalty percentage on the ticket price.
                    - **`Amount`**: (`decimal`). Total penalty amount that will be applied.
                    - **`FromInclusiveDateTime`**: (`dateTime`). Date/time from which this rule will apply.
                    - **`ToExclusiveDateTime`**: (`dateTime`). Date/time until which this rule will apply.

- **`Accommodations`**: (`list`). Information about accommodations/rooms added to the cart.
    - **`Accommodation`**: (`object`). Accommodation information.
        - **`ProductId`**: (`string`). Rate identifier.
        - **`ProductConditions`**: (`string`). Product conditions.
        - **`AccessDateTime`**: (`dateTime`). Check-in date.
        - **`AccessEndDateTime`**: (`dateTime`). Check-out date.
        - **`Quantity`**: (`int`). Quantity of units added.
        - **`Price`**: (`decimal`). Rate price.
        - **`PriceMode`**: (`int`). Price type.

            ??? example "Possible values"
                --8<-- "includes/enum/priceMode.en.md"

        - **`Success`**: (`boolean`). Indicates whether the reservation was made successfully.
        - **`ErrorMessage`**: (`boolean`). In case of reservation error, associated message.
        - **`ChildrenAges`**: (`list`). List of the ages of babies/children.
            - **`int`**: Age of the baby/child.
        - **`NumberOfAdults`**: (`int`). Number of adults in this room.
        - **`NumberOfChildren`**: (`int`). Number of children in this room.
        - **`NumberOfSenior`**: (`int`). Number of seniors in this room.
        - **`NumberOfBabies`**: (`int`). Number of babies in this room.
        - **`NumberOfGeneric`**: (`int`). Number of undefined persons in this room.
        - **`CancellationPolicy`**: (`object`). Indicates the cancellation policies that apply when cancelling this product.
            - **`IsRefundable`**: (`boolean`). Indicates whether free cancellation is available at any point.
            - **`Rules`**: (`list`). List of rules applied when cancelling.
                - **`Rule`**: Information about the rule to apply.
                    - **`HoursInAdvanceOfAccess`**: (`int`). Number of hours in advance with respect to the access date from which the penalty indicated in `Percentage` will be applied.
                    - **`Percentage`**: (`decimal`). Penalty percentage on the ticket price.
                    - **`Amount`**: (`decimal`). Total penalty amount that will be applied.
                    - **`FromInclusiveDateTime`**: (`dateTime`). Date/time from which this rule will apply.

- **`PaymentMethodsNotApplicable`**: (`boolean`). Indicates whether payment methods apply to this partner. Partners with a debit contract will need to apply payment methods (`#!csharp PaymentMethodsNotApplicable = false`).
- **`PaymentMethods`**: (`list`). Payment methods supported for the partner if working in debit mode.
    - **`PaymentMethod`**: (`object`). Information about the payment method.
        - **`Id`**: (`string`). Payment method identifier.
        - **`Type`**: (`byte`). Payment method type.
        - **`Name`**: (`string`). Payment method name.
        - **`CommercialName`**: (`string`) `Optional`. Commercial name of the payment method.
        - **`EnableSendByEmail`**: (`boolean`) `Optional`. Indicates whether this payment method can be used to automatically send a payment link by email.
        - **`Fields`**: (`list`). Array of fillable fields associated with the payment method. These fields can be specified when creating a transaction.
            - **`Id`**: (`string`). Field identifier.
            - **`Name`**: (`string`). Field name.
            - **`IsRequired`**: (`boolean`). Indicates whether the field is mandatory.
            - **`RegexValidation`**: (`string`) `Optional`. Regular expression that the field value must satisfy.
            - **`RegexValidationErrorMessage`**: (`string`) `Optional`. Error message to display if the regular expression is not satisfied.
            - **`DefaultValue`**: (`string`) `Optional`. Default field value to show to the user.
            - **`DataType`**: (`byte`). Indicates the data type required by the field value.

                ??? example "Possible values"
                    - 0: Text
                    - 1: Numeric
                    - 2: Date
                    - 3: Boolean

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response examples

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/confirm.response.1.md"

## Additional HTTP headers

- This call accepts an additional header to indicate the partner user who is performing the cart confirmation:

  | Header name          | Header value                   |
  |----------------------|--------------------------------|
  | `AdminPartnerUserId` | `AdminPartner user identifier` |
