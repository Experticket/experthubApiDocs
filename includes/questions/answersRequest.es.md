- **`QuestionsProfiles`**: (``list``) ``Opcional``. Listado de perfiles de preguntas con sus respuestas. Se utiliza para responder a las preguntas de nivel **venta**, **proveedor** y **cliente**. Las preguntas de nivel **ticket** se responden al [añadir el producto al carrito](add.md), no aquí. Consulta la [introducción a los perfiles de preguntas](../activity/questions.md) para entender cada nivel.
    - **`QuestionsProfileId`**: (``string``) ``Requerido``. Identificador del perfil de preguntas. Se obtiene del [catálogo](../activity/catalog.md) (`SaleQuestionProfileIds`, `ClientQuestionProfileIds`, `ProviderQuestionsProfileIds`) y de [consultar perfiles de preguntas](../activity/CheckTicketsQuestions.md).
    - **`Questions`**: (``list``) ``Requerido``. Respuestas a las preguntas del perfil.
        - **`QuestionId`**: (``string``) ``Requerido``. Identificador de la pregunta (campo `Id` de la pregunta devuelto al [consultar perfiles de preguntas](../activity/CheckTicketsQuestions.md)).
        - **`Question`**: (``string``) ``Opcional``. Texto de la pregunta. Informativo.
        - **Propiedad de valor**: según el `DataType` de la pregunta, debe rellenarse **una** de las siguientes propiedades:
            - **`StringValue`** (``string``) / **`StringCollectionValue`** (``list``).
            - **`BooleanValue`** (``boolean``) / **`BooleanCollectionValue`** (``list``).
            - **`IntegerValue`** (``int``) / **`IntegerCollectionValue`** (``list``).
            - **`DecimalValue`** (``decimal``) / **`DecimalCollectionValue`** (``list``).
            - **`DateTimeValue`** (``dateTime``) / **`DateTimeCollectionValue`** (``list``).
            - **`BinaryValue`** (``string``) / **`BinaryCollectionValue`** (``list``). Contenido del archivo codificado en base64.
        - **`BinaryMimeType`**: (``string``) ``Opcional``. Tipo MIME del archivo. Solo para `DataType` = 12 o 13.
        - **`BinaryExtension`**: (``string``) ``Opcional``. Extensión del archivo. Solo para `DataType` = 12 o 13.

    ??? example "Tipo de dato (`DataType`) → propiedad de respuesta"
        --8<-- "includes/enum/questionDataType.es.md"
