- **`Id`**: (``string``). Identificador del perfil de preguntas. Coincide con el identificador expuesto en el [catálogo](catalog.md) (`TicketsQuestionsProfileId`, `ProviderQuestionsProfileIds`, `SaleQuestionProfileIds`, `SaleTravelQuestionProfileIds` o `ClientQuestionProfileIds` según el nivel).
- **`Name`**: (``string``). Nombre del perfil.
- **`CommercialName`**: (``string``) ``Opcional``. Nombre comercial del perfil.
- **`AreDynamicQuestions`**: (``boolean``). Indica si el perfil contiene preguntas **dinámicas**. Si es `#!csharp true`, las preguntas se generan en tiempo real a partir de la integración del proveedor y, para obtenerlas, la consulta debe incluir los productos con su fecha de acceso. Si es `#!csharp false`, el perfil contiene preguntas **estáticas** definidas en configuración. Consulta [tipos de preguntas](questions.md#tipos-de-preguntas).
- **`Questions`**: (``list``). Lista de preguntas que componen el perfil.
    - **`Id`**: (``string``). Identificador de la pregunta. Es el valor que debe enviarse como `QuestionId` al responder.
    - **`Question`**: (``string``). Texto principal de la pregunta.
    - **`ShortQuestion`**: (``string``). Texto abreviado de la pregunta.
    - **`Required`**: (``boolean``). Indica si la respuesta a la pregunta es obligatoria.
    - **`DataType`**: (``byte``). Tipo de dato de la pregunta. Determina en qué propiedad debe enviarse la respuesta.

        ??? example "Posibles valores"
            --8<-- "includes/enum/questionDataType.es.md"

    - **`MaxNumberOfValues`**: (``int``) ``Opcional``. Solo para `DataType` = 11 (selección múltiple). Número máximo de valores que se pueden seleccionar.
    - **`RegexValidationPattern`**: (``string``) ``Opcional``. Expresión regular que debe cumplir la respuesta.
    - **`RegexValidationErrorMessage`**: (``string``) ``Opcional``. Mensaje de error a mostrar al usuario cuando la respuesta no cumple la expresión regular.
    - **`Values`**: (``list``) ``Opcional``. Solo para `DataType` = 10 u 11. Conjunto de valores predefinidos entre los que elegir.
        - **`Text`**: (``string``). Texto a mostrar al usuario.
        - **`Value`**: (``string``). Valor que debe enviarse como respuesta.
