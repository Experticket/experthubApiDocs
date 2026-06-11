- **`QuestionsProfiles`**: (`list`) `Optional`. List of question profiles with their answers. Used to answer questions at the **sale**, **provider** and **client** levels. **Ticket** level questions are answered when [adding the product to the cart](add.md), not here. See the [introduction to question profiles](../activity/questions.md) to understand each level.
    - **`QuestionsProfileId`**: (`string`) `Required`. Question profile identifier. It is obtained from the [catalog](../activity/catalog.md) (`SaleQuestionProfileIds`, `ClientQuestionProfileIds`, `ProviderQuestionsProfileIds`) and from [checking question profiles](../activity/CheckTicketsQuestions.md).
    - **`Questions`**: (`list`) `Required`. Answers to the profile questions.
        - **`QuestionId`**: (`string`) `Required`. Question identifier (the question's `Id` field returned by [checking question profiles](../activity/CheckTicketsQuestions.md)).
        - **`Question`**: (`string`) `Optional`. Question text. Informational.
        - **Value property**: depending on the question's `DataType`, **one** of the following properties must be filled in:
            - **`StringValue`** (`string`) / **`StringCollectionValue`** (`list`).
            - **`BooleanValue`** (`boolean`) / **`BooleanCollectionValue`** (`list`).
            - **`IntegerValue`** (`int`) / **`IntegerCollectionValue`** (`list`).
            - **`DecimalValue`** (`decimal`) / **`DecimalCollectionValue`** (`list`).
            - **`DateTimeValue`** (`dateTime`) / **`DateTimeCollectionValue`** (`list`).
            - **`BinaryValue`** (`string`) / **`BinaryCollectionValue`** (`list`). File content encoded in base64.
        - **`BinaryMimeType`**: (`string`) `Optional`. File MIME type. Only for `DataType` = 12 or 13.
        - **`BinaryExtension`**: (`string`) `Optional`. File extension. Only for `DataType` = 12 or 13.

    ??? example "Data type (`DataType`) → answer property"
        --8<-- "includes/enum/questionDataType.en.md"
