- **`Id`**: (`string`). Question profile identifier. It matches the identifier exposed in the [catalog](catalog.md) (`TicketsQuestionsProfileId`, `ProviderQuestionsProfileIds`, `SaleQuestionProfileIds` or `ClientQuestionProfileIds` depending on the level).
- **`Name`**: (`string`). Profile name.
- **`CommercialName`**: (`string`) `Optional`. Commercial name of the profile.
- **`AreDynamicQuestions`**: (`boolean`). Indicates whether the profile contains **dynamic** questions. If `#!csharp true`, the questions are generated in real time from the provider's integration and, to retrieve them, the query must include the products with their access date. If `#!csharp false`, the profile contains **static** questions defined in configuration. See [question types](questions.md#question-types).
- **`Questions`**: (`list`). List of questions that make up the profile.
    - **`Id`**: (`string`). Question identifier. This is the value that must be sent as `QuestionId` when answering.
    - **`Question`**: (`string`). Main question text.
    - **`ShortQuestion`**: (`string`). Short question text.
    - **`Required`**: (`boolean`). Indicates whether answering the question is mandatory.
    - **`DataType`**: (`byte`). Question data type. Determines which property the answer must be sent in.

        ??? example "Possible values"
            --8<-- "includes/enum/questionDataType.en.md"

    - **`MaxNumberOfValues`**: (`int`) `Optional`. Only for `DataType` = 11 (multiple selection). Maximum number of values that can be selected.
    - **`RegexValidationPattern`**: (`string`) `Optional`. Regular expression that the answer must match.
    - **`RegexValidationErrorMessage`**: (`string`) `Optional`. Error message to show the user when the answer does not match the regular expression.
    - **`Values`**: (`list`) `Optional`. Only for `DataType` = 10 or 11. Set of predefined values to choose from.
        - **`Text`**: (`string`). Text to show the user.
        - **`Value`**: (`string`). Value that must be sent as the answer.
