# CheckTicketsQuestions

Con este método se puede realizar consultas para conocer las necesidades que pueden llegar a tener los tickets.

Gracias a ello, si realizamos una llamada a este método veremos en la respuesta dicha información en modo de preguntas con sus respectivas indicaciones que anteriormente de definieron para su uso.

## Método de acceso

**POST** actvity/checkticketsquestions

## Estructura de la petición

Para generar la estructura de petición, debemos generar un objecto con los campos que a continuación se nombran.

- **`ProductIds`**: (``list``). Array de identificadores de productos.
- **`TicketsQuestionsProfileIds`**: (``list``). Array de perfiles de las preguntas correspondientes al ticket.
- **`LanguageCode`**: (``list``). Código del idioma.

### Ejemplos de petición

--8<-- "includes/examples/activity/CheckTicketsQuestionsQueryExamples.md"

## Estructura de la respuesta

Como respuesta a la llamada a este método se devolverá una estructura muy similar a la de envío, pero añadiendo algunos campos nuevos.

- **`Products`**: (``list``). Lista de productos.
    - **`ProductId`**: (``string``). Identificador del producto.
    - **`Tickets`**: (``list``). Lista de tickets.
        - **`TicketId`**: (``string``). Identificador del ticket.
        - **`TicketQuestionsProfileId`**: (``string``). Identificador del perfil de la pregunta.
  
- **`TicketQuestionsProfiles`**: (``list``). Lista con los perfiles de las preguntas.
    - **`Id`**: (``string``). Identificador.
    - **`Questions`**: (``list``). Lista con las preguntas correspondientes.
        - **`Id`**: (``string``). Identificador de la pregunta.
        - **`Question`**: (``string``). Pregunta principal
        - **`ShortQuestion`**: (``string``). Pregunta abreviada.
        - **`Required`**: (``boolean``). Indica si es obligatoria la pregunta.
        - **`DataType`**: (``numeric``). Tipología de la pregunta, puede tomar los siguientes valores</a>.

            ??? example "Posibles valores"
                - 0: Texto
                - 2: Booleano
                - 4: Fecha
                - 6: Número entero
                - 8: Número decimal
                - 10: Selección de un valor entre un conjunto de valores predefinidos.
                - 11: Selección de varios valores entre un conjunto de valores predefinidos.
                - 12: Archivo.

        - **`Values`**: (``string``). Array con los valores correspondientes.

--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplos de respuesta

--8<-- "includes/examples/activity/CheckTicketsQuestionsResponseExamples.md"
