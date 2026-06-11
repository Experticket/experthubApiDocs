# Check question profiles

This method retrieves the **question profiles** and their questions for the different levels: ticket, provider, sale, travel and client. For each question, the response includes its text, whether it is mandatory, its data type, validations and possible predefined values.

!!! tip "Before you start"
    It is advisable to read the [introduction to question profiles](questions.md), which explains the levels, the types (static/dynamic and public/private) and the full API flow.

The profile identifiers queried here are obtained beforehand from the [catalog](catalog.md): `TicketsQuestionsProfileId` (ticket), `ProviderQuestionsProfileIds` (provider) and `SaleQuestionProfiles` (sale, travel and client).

## Access method

**POST** /activity/checkticketsquestions

## Request structure

To build the request, create an object with the following fields. All are optional, but at least one source of profiles must be provided (`QuestionsProfileIds` or `Products`).

- **`QuestionsProfileIds`**: (`list`) `Optional`. Array of question profile identifiers to query (of any level).
- **`Products`**: (`list`) `Optional`. List of products for which to retrieve the questions. It is **mandatory** to retrieve **dynamic questions**, since they depend on the product and the access date. See [question types](questions.md#question-types).
    - **`ProductId`**: (`string`) `Required`. Product identifier.
    - **`AccessDate`**: (`date`) `Required`. Access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **`Tickets`**: (`list`) `Optional`. Product tickets for which to retrieve the ticket questions.
        - **`TicketId`**: (`string`) `Required`. Ticket identifier.
        - **`SessionId`**: (`string`) `Optional`. Session identifier.
        - **`AccessDate`**: (`date`) `Optional`. Ticket access date. *ISO 8601 format (yyyy-MM-dd)*.
- **`IncludeSaleTravelQuestionsProfiles`**: (`boolean`) `Optional`. If `#!csharp true`, the response will include the **travel** level profiles (`SaleTravelQuestionsProfiles`). Defaults to `#!csharp false`.
- **`LanguageCode`**: (`string`) `Optional`. Language in which the question texts will be returned. *ISO 639-1 format*.

!!! note "Provider questions by session"
    Some provider questions are only returned if the session (`SessionId`) is indicated in the tickets sent in `Products`.

### Request examples

--8<-- "includes/examples/activity/CheckTicketsQuestionsQueryExamples.md"

## Response structure

The response groups profiles by level. It also includes two mapping lists (`Products` and `Providers`) that relate each queried entity to its profiles.

- **`Products`**: (`list`). Relates each queried product/ticket to its ticket question profile.
    - **`ProductId`**: (`string`). Product identifier.
    - **`AccessDate`**: (`dateTime`) `Optional`. Access date.
    - **`ProviderId`**: (`string`). Identifier of the product's provider.
    - **`Tickets`**: (`list`). List of tickets.
        - **`TicketId`**: (`string`). Ticket identifier.
        - **`SessionId`**: (`string`) `Optional`. Session identifier.
        - **`TicketQuestionsProfileId`**: (`string`). Ticket question profile identifier.
        - **`AccessDate`**: (`dateTime`) `Optional`. Ticket access date.
- **`Providers`**: (`list`). Relates each queried provider to its provider question profiles.
    - **`ProviderId`**: (`string`). Provider identifier.
    - **`ProviderQuestionsProfileIds`**: (`list`). Array of question profile identifiers associated with the provider.
- **`TicketQuestionsProfiles`**: (`list`). **Ticket** level question profiles.
- **`ProviderQuestionsProfiles`**: (`list`). **Provider** level question profiles.
- **`SaleQuestionsProfiles`**: (`list`). **Sale** level question profiles.
- **`SaleTravelQuestionsProfiles`**: (`list`). **Travel** level question profiles. Returned only if the request sets `IncludeSaleTravelQuestionsProfiles = true`.
- **`ClientQuestionsProfiles`**: (`list`). **Client** level question profiles.

All profile lists (`TicketQuestionsProfiles`, `ProviderQuestionsProfiles`, `SaleQuestionsProfiles`, `SaleTravelQuestionsProfiles` and `ClientQuestionsProfiles`) share the following **profile** structure:

--8<-- "includes/questions/profileResponse.en.md"

--8<-- "includes/responseBaseDocumentation.en.md"

### Response examples

Example with profiles of several levels (ticket, provider, sale and client):

--8<-- "includes/examples/activity/CheckQuestionsAllLevelsResponseExample.md"

Examples of a question node depending on its data type:

--8<-- "includes/examples/activity/CheckTicketsQuestionsResponseExamples.md"
