# CheckTicketsQuestions

This method allows queries to determine which requirements tickets may have.

Thanks to this, when we call this method, the response will return the information as questions together with the indications that were previously defined for their use.

## Access method

**POST** /activity/checkticketsquestions

## Request structure

To generate the request structure, an object must be sent with the following fields.

- **`ProductIds`**: (`list`). Array of product identifiers.
- **`TicketsQuestionsProfileIds`**: (`list`). Array of question profile identifiers associated with the ticket.
- **`LanguageCode`**: (`list`). Language code.

### Request examples

--8<-- "includes/examples/activity/CheckTicketsQuestionsQueryExamples.md"

## Response structure

The response structure is very similar to the request, but includes some additional fields.

- **`Products`**: (`list`). List of products.
    - **`ProductId`**: (`string`). Product identifier.
    - **`Tickets`**: (`list`). List of tickets.
        - **`TicketId`**: (`string`). Ticket identifier.
        - **`TicketQuestionsProfileId`**: (`string`). Question profile identifier.

- **`TicketQuestionsProfiles`**: (`list`). List of question profiles.
    - **`Id`**: (`string`). Identifier.
    - **`Questions`**: (`list`). List of the corresponding questions.
        - **`Id`**: (`string`). Question identifier.
        - **`Question`**: (`string`). Main question.
        - **`ShortQuestion`**: (`string`). Short question.
        - **`Required`**: (`boolean`). Indicates whether the question is mandatory.
        - **`DataType`**: (`numeric`). Question data type. It can take the following values.

            ??? example "Possible values"
                - 0: Text
                - 2: Boolean
                - 4: Date
                - 6: Integer number
                - 8: Decimal number
                - 10: Select one value from a predefined set of values.
                - 11: Select multiple values from a predefined set of values.
                - 12: File.

        - **`Values`**: (`string`). Array with the corresponding values.

--8<-- "includes/responseBaseDocumentation.en.md"

### Response examples

--8<-- "includes/examples/activity/CheckTicketsQuestionsResponseExamples.md"
