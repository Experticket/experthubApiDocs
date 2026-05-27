# Add items to the cart

This method allows us to add activities, accommodations, and/or packages to the shopping cart.

It can be called one or more times, depending on how we need to keep adding items to the cart.

We can add one or several products in one or several calls, depending on the needs of the integration process.

## Access method

**POST** /ShoppingCart/Add

## Request structure

- **`ShoppingCartId`**: (`string`) `Required`. Cart identifier.
- **`Activities`**: (`list`) `Optional`. List of activities to add to the cart.
    - **`Activity`**: (`object`) `Optional`. Activity information.
        - **`ProductId`**: (`string`) `Required`. Product identifier.
        - **`CombinedProductId`**: (`string`) `Optional`. Combined product identifier.
        - **`GiftCardIdentifier`**: (`string`) `Optional`. Identifier of the gift card being redeemed.
        - **`AccessDateTime`**: (`date`) `Required`. Access date. ISO 8601 format (yyyy-MM-dd).
        - **`Quantity`**: (`int`) `Required`. Product quantity.
        - **`Tickets`**: (`object`) `Optional`. List containing ticket information.
            - **`TicketId`**: (`string`) `Required`. Ticket identifier.
            - **`SessionId`**: (`string`) `Optional`. Session identifier.
            - **`AccessDateTime`**: (`date`) `Required`. Access date. ISO 8601 format (yyyy-MM-dd).
            - **`Questions`**: (`list`) `Optional`. List of answers to ticket questions.
                - **`QuestionId`**: (`string`) `Required`. Question identifier.
                - **`StringValue`**: (`string`) `Required`. Answer to the question.

                ??? info "Additional information"
                    - When any of the tickets of the catalog products we want to add to the cart has the `TicketsQuestionsProfileId` property filled in, we must check [ticket questions](../activity/CheckTicketsQuestions.md) to know which ticket questions that activity has.
                    - Depending on the question type, the answer value must be sent in one property or another. For example, if the question is text type (`DataType` = 0), the `StringValue` property must be filled in.
                    - Another example: if the question is date type (`DataType` = 4), then `DateTimeValue` must be filled in, and so on.
                    ??? example "Possible values"
                        --8<-- "includes/enum/examenResponseQuestions.md"

- **`GiftCards`**: (`list`) `Optional`. List of gift cards to add to the cart.
    - **`ProductIds`**: (`list`). List of activity identifiers included in the gift card.
        - **`(string)`**: Activity identifier.
    - **`AccessDateTime`**: (`date`) `Required`. Approximate access date. It is only used for statistical purposes; the customer who redeems the card will be able to choose the actual access dates. ISO 8601 format (yyyy-MM-dd).
    - **`Message`**: (`string`) `Optional`. Message from the purchaser to the person who will redeem the gift card.
    - **`Client`**: (`object`) `Optional`. Data of the customer who will redeem the gift card.
        - **`FullName`**: (`string`) `Optional`. Name.
        - **`Email`**: (`string`) `Optional`. If this field is provided, the person redeeming the gift card will receive it by email.

- **`Accommodations`**: (`list`) `Optional`. List of accommodations to add to the cart.
    - **`Accommodation`**: (`object`) `Optional`. Accommodation information.
        - **`EchoToken`**: (`string`) `Required`. Token obtained in the accommodation request.
        - **`Rates`**: (`list`) `Required`. List of rate identifiers.
            - **`(string)`**: `Required`. Rate identifier.
- **`Packages`**: (`list`) `Optional`. List of package groupings to add to the cart.
    - **`Package`**: (`object`) `Optional`. Package group information.
        - **`EchoToken`**: (`string`) `Required`. Token obtained in the package request.
        - **`Packages`**: (`list`) `Required`. List of packages.
            - **`Package`**: (`object`) `Required`. Package information.
                - **`Id`**: `Required`. Package identifier.
                - **`Providers`**: (`list`) `Optional`. Object with provider data.
                    - **`Id`**: (`string`) `Required`. Identifier.
                    - **`Activities`**: (`list`) `Optional`. List of activities to add to the cart.
                        - **`Id`**: (`string`) `Required`. Identifier.
                        - **`ProductBaseId`**: (`string`) `Required`. Product base identifier.
                        - **`Tickets`**: (`object`) `Optional`. List containing ticket information.
                            - **`SessionId`**: (`string`) `Optional`. Session identifier.
                            - **`AccessDateTime`**: (`date`) `Required`. Session date.
                            - **`TicketId`**: (`string`) `Optional`. Ticket identifier.

### Request examples

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/add.request.1.md"

## Response structure

It is important to take into account the **`Id`** properties returned in the response, because they will be needed to manipulate the products once they have been added to the cart.

- **`Activities`**: (`list`). List of activities added in the **current request**. If no activities were added, this property will not appear.
    - **`Activity`**: (`object`). Information about the added activity.
        - **`Id`**: (`string`). Identifier assigned to this activity inside the cart.
        - **`Activity`**: (`object`). Information about the added activity.
            - **`ProductId`**: (`string`). Product identifier.
            - **`Quantity`**: (`int`). Added quantity.
            - **`AccessDateTime`**: (`dateTime`). Access date. ISO 8601 format (yyyy-MM-ddThh\:mm\:ss).
            - **`ForceNotAutoAssignSeating`**: (`boolean`). Force assigned seating.
            - **`Tickets`**: (`list`). List of tickets.
                - **`TicketId`**: (`string`). Ticket identifier.
                - **`SessionId`**: (`string`). Session identifier.
                - **`Questions`**: (`object`). Information about the questions.
                    - **`TicketQuestionId`**: (`string`). Question identifier.
                    - **`Question`**: (`string`). Question.
                    - **`StringValue`**: (`string`). Question answer.

                    ??? info "Additional information"
                        - Depending on the question type, the response value is returned in one property or another. For example, if the question is text type (`DataType` = 0), the `StringValue` property will be returned.
                        - Another example: if the question is date type (`DataType` = 4), then the `DateTimeValue` property will be returned, and so on.
                        ??? example "Possible values"
                            --8<-- "includes/enum/examenResponseQuestions.md"

- **`Accommodations`**: (`list`). List of accommodations added in the **current request**. If no accommodations were added, this property will not appear.
    - **`Accommodation`**: (`object`). Information about the added accommodation.
        - **`Id`**: (`string`). Identifier assigned to this accommodation inside the cart.
        - **`RateId`**: (`string`). Rate identifier.

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response examples

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/add.response.1.md"
