# Gift cards

Gift cards can be created by adding as many activities from the [activities catalog](catalog.md) as needed. The data structure used to add gift cards to the cart is described in the [add to cart](../shoppingCart/add.md) section.

After purchasing the gift card, a unique code is generated so that it can be redeemed. The dates and sessions, if applicable, of the included activities are chosen at redemption time.

To perform the redemption process, the products included in the gift card are added to the cart indicating the gift card code they belong to. The data structure used to indicate that an activity belongs to a gift card is described in the [add to cart](../shoppingCart/add.md) section.

## Check gift card

Using this method, we can check whether a gift card can be redeemed from a redemption code.

## Access method

**GET** /activity/giftcard

## Request structure

- **`GiftCardIdentifier`**: (`string`). Redemption code.
- **`LanguageCode`**: (`string`) `Optional`. Defines the language in which the texts will be displayed. By default, the language configured for the partner will be returned.

### Request example

--8<-- "includes/examples/activity/giftCardQueryExamples.md"

## Response structure

- **`GiftCardIdentifier`**: (`string`). Redemption code.
- **`SaleId`**: (`string`). Sale identifier.
- **`PartnerSaleId`**: (`string`). Partner identifier.
- **`IsExchanged`**: (`boolean`). Indicates whether the gift card has already been redeemed.
- **`HoursInAdvanceOfGiftCardExchange`**: (`short`). Hours in advance required for redemption compared with 00:00 of the day after the visit.
- **`Message`**: (`string`). Message from the gift card purchaser to the person redeeming it.
- **`Client`**: (`object`). Data of the customer who will redeem the card.
    - **`CreatedDate`**: (`dateTime`). Date when the customer record was created.
    - **`FullName`**: (`string`). Name.
    - **`Surname`**: (`string`). Surname.
    - **`CountryCode`**: (`string`). Country code.
    - **`LanguageCode`**: (`string`). Language code.
    - **`Gender`**: (`byte`). Gender.
    - **`AcceptsEmailContact`**: (`boolean`). Accepts receiving marketing communications.
    - **`AllowCustomerProfiling`**: (`boolean`). Accepts the creation of a customer profile.
--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/activity/giftCardResponseExamples.md"
