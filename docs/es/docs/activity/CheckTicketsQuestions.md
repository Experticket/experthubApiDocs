# Consultar perfiles de preguntas

Con este método se obtienen los **perfiles de preguntas** y sus preguntas para los distintos niveles: ticket, proveedor, venta y cliente. La respuesta incluye, por cada pregunta, su texto, obligatoriedad, tipo de dato, validaciones y posibles valores predefinidos.

!!! tip "Antes de empezar"
    Conviene leer la [introducción a los perfiles de preguntas](questions.md), que explica los niveles, los tipos (estáticas/dinámicas y públicas/privadas) y el flujo completo en la API.

Los identificadores de perfil que se consultan aquí se obtienen previamente del [catálogo](catalog.md): `TicketsQuestionsProfileId` (ticket), `ProviderQuestionsProfileIds` (proveedor) y `SaleQuestionProfiles` (venta y cliente).

## Método de acceso

**POST** /activity/checkticketsquestions

## Estructura de la petición

Para generar la petición se construye un objeto con los siguientes campos. Todos son opcionales, pero debe indicarse al menos un origen de perfiles (`QuestionsProfileIds` o `Products`).

- **`QuestionsProfileIds`**: (``list``) ``Opcional``. Array de identificadores de perfiles de preguntas a consultar (de cualquier nivel).
- **`Products`**: (``list``) ``Opcional``. Lista de productos para los que se quieren obtener las preguntas. Es **imprescindible** para obtener **preguntas dinámicas**, ya que dependen del producto y de la fecha de acceso. Ver [tipos de preguntas](questions.md#tipos-de-preguntas).
    - **`ProductId`**: (``string``) ``Requerido``. Identificador del producto.
    - **`AccessDate`**: (``date``) ``Requerido``. Fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **`Tickets`**: (``list``) ``Opcional``. Tickets del producto para los que obtener las preguntas de ticket.
        - **`TicketId`**: (``string``) ``Requerido``. Identificador del ticket.
        - **`SessionId`**: (``string``) ``Opcional``. Identificador de la sesión.
        - **`AccessDate`**: (``date``) ``Opcional``. Fecha de acceso del ticket. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`LanguageCode`**: (``string``) ``Opcional``. Idioma en que se devolverán los textos de las preguntas. *Formato ISO 639-1*.

!!! note "Preguntas de proveedor por sesión"
    Algunas preguntas de proveedor **dinámicas** solo se devuelven si se indica la sesión (`SessionId`) en los tickets enviados en `Products`.

### Ejemplos de petición

--8<-- "includes/examples/activity/CheckTicketsQuestionsQueryExamples.md"

## Estructura de la respuesta

La respuesta agrupa los perfiles por nivel. Además, incluye dos listas de mapeo (`Products` y `Providers`) que relacionan cada entidad consultada con sus perfiles.

- **`Products`**: (``list``). Relaciona cada producto/ticket consultado con su perfil de preguntas de ticket.
    - **`ProductId`**: (``string``). Identificador del producto.
    - **`AccessDate`**: (``dateTime``) ``Opcional``. Fecha de acceso.
    - **`ProviderId`**: (``string``). Identificador del proveedor del producto.
    - **`Tickets`**: (``list``). Lista de tickets.
        - **`TicketId`**: (``string``). Identificador del ticket.
        - **`SessionId`**: (``string``) ``Opcional``. Identificador de la sesión.
        - **`TicketQuestionsProfileId`**: (``string``). Identificador del perfil de preguntas del ticket.
        - **`AccessDate`**: (``dateTime``) ``Opcional``. Fecha de acceso del ticket.
- **`Providers`**: (``list``). Relaciona cada proveedor consultado con sus perfiles de preguntas de proveedor.
    - **`ProviderId`**: (``string``). Identificador del proveedor.
    - **`ProviderQuestionsProfileIds`**: (``list``). Array de identificadores de perfiles de preguntas asociados al proveedor.
- **`TicketQuestionsProfiles`**: (``list``). Perfiles de preguntas de nivel **ticket**.
- **`ProviderQuestionsProfiles`**: (``list``). Perfiles de preguntas de nivel **proveedor**.
- **`SaleQuestionsProfiles`**: (``list``). Perfiles de preguntas de nivel **venta**.
- **`ClientQuestionsProfiles`**: (``list``). Perfiles de preguntas de nivel **cliente**.

Todas las listas de perfiles (`TicketQuestionsProfiles`, `ProviderQuestionsProfiles`, `SaleQuestionsProfiles` y `ClientQuestionsProfiles`) comparten la siguiente estructura de **perfil**:

--8<-- "includes/questions/profileResponse.es.md"

--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplos de respuesta

Ejemplo con perfiles de varios niveles (ticket, proveedor, venta y cliente):

--8<-- "includes/examples/activity/CheckQuestionsAllLevelsResponseExample.md"

Ejemplos del nodo de una pregunta según su tipo de dato:

--8<-- "includes/examples/activity/CheckTicketsQuestionsResponseExamples.md"
