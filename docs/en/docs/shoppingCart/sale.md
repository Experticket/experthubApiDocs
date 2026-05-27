# Confirm the reservation

This method confirms the reservation previously made in our systems.

## Access method

**POST** /ShoppingCart/Sale

## Request structure

- **`ShoppingCartId`**: (`string`) `Required`. Cart identifier.
- **`PartnerSaleId`**: (`string`) `Required`. Partner identifier.
- **`InsurancePolicyId`**: (`string`) `Optional`. Refund insurance policy identifier.

    ??? tip "Information"
        This identifier is obtained when calling [check available policies](../activity/checkInsurancePolicies.md). That function returns a list of available policies with their identifiers (`Id`). That is the identifier that must be used in this field.

- **`DiscountCouponCodes`**: (`list`) `Optional`. List of coupon codes (discounts/promotions) issued by the venue through this platform.
    - **`(string)`**: (`list`) `Required`. Coupon code.
- **`Client`**: (`object`) `Optional`. Customer information. If the sale contains hotels, this property is mandatory. If it only contains activities, this parameter depends on the configuration agreed with the partner.
    - **`FullName`**: (`string`) `Required`. Name.
    - **`Surname`**: (`string`) `Required`. Surname.
    - **`DocumentIdentifier`**: (`string`) `Required`. Identity document.
    - **`PhoneNumber`**: (`string`) `Required`. Phone number.
    - **`Email`**: (`string`) `Required`. Email address.
- **`PaymentMethod`**: (`string`) `Optional`. Payment method information. It only needs to be filled in when the partner has a debit contract.
    - **`PaymentMethodType`**: (`int`) `Required`. Payment method identifier.
    - **`ReturnUrlOk`**: (`string`) `Required`. URL that will be notified if the payment succeeds.
    - **`ReturnUrlKo`**: (`string`) `Required`. URL that will be notified if the payment fails.
    - **`SendByEmail`**: (`boolean`) `Required`. Indicates that we want to send the customer a payment link by email, if the option is available. See [PaymentMethods.PaymentMethod.EnableSendByEmail](./confirm.md#response-structure).

### Request example

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/sale.request.1.md"

## Response structure

- **`PaymentRedirectUrl`**: (`string`). For partners with debit payment, this property indicates the URL where the customer must be redirected to complete the payment.
- **`ExperticketSales`**: (`list`). List of associated sales.
    - **`ExperticketSale`**: (`object`). Sale information.
        - **`Id`**: (`string`). Sale identifier.
            - **`FinancialRatios`**: (`object`). Economic concepts of a sale.
                - **`ReferenceSalePrice`**: (`object`). Reference sale price.
                    --8<-- "includes/annex/financialRatios.en.md"
                - **`Discount`**: (`object`). Commercial discount.
                    --8<-- "includes/annex/financialRatios.en.md"
                - **`Commission`**: (`object`). Partner cost.
                    --8<-- "includes/annex/financialRatios.en.md"
                - **`SalePrice`**: (`object`). Sale price.
                    --8<-- "includes/annex/financialRatios.en.md"

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response example

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/sale.response.1.md"

## Additional HTTP headers

- This call accepts an additional header to indicate the partner user who is performing the sale:

  | Header name          | Header value                   |
  |----------------------|--------------------------------|
  | `AdminPartnerUserId` | `AdminPartner user identifier` |
