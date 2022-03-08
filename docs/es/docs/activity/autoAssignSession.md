# Comprobar sesiones auto asignadas

Pueden existir productos cuyas sesiones no pueden ser elegidas o no es obligatorio elegirlas, en este caso es el sistema el que asigna las sesiones según la disponibilidad.

Para saber si un producto tiene sesiones auto asignadas se comprueba mirando en el [catálogo](catalog.md) la propiedad **``TicketEnclosureAutoAssignSessionType``** del nodo de sesiones del recinto.

??? example "Posibles valores de TicketEnclosureAutoAssignSessionType"
    --8<-- "includes/annex/autoAssignSessionType.es.md"

Una vez lanzada la consulta se devolverá, a modo informativo, la sesión que se asignará cuando se confirme el carrito.

!!! warning "La sesión obtenida puede no ser la sesión asignada en el momento de confirmar el carrito."

## Método de acceso

**POST** /autoassignsessions

## Estructura de la petición

- **`LanguageCode`**: define el idioma en que se mostrarán los textos. *Formato ISO 639-1*.
- **`Products`**: array de productos para los que se quieren comprobar las sesiones.
    - **`ProductId`**: identificador del producto.
    - **`Quantity`**: cantidad del producto.
    - **`AccessDate`**: fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **`Tickets`**: array de tickets para los que queremos comprobar la auto asignación.
        - **`TicketId`**: identificador del ticket.
        - **`AccessDate`**: *opcional*, si se indica, tiene preferencia sobre la fecha indicada a nivel de producto. *Formato ISO 8601 (yyyy-MM-dd)*.

### Ejemplo de petición

--8<-- "includes/examples/activity/autoAssignSessionQueryExamples.md"

## Estructura de la respuesta

- **`Products`**: array que contiene los productos solicitados.
    - **`ProductId`**: identificador del producto.
    - **`AccessDate`**: fecha de acceso del producto. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **`HasTicketEnclosures`**: booleano que indica si el producto tiene recintos.
    - **`Tickets`**: array de los tickets solicitados del producto.
        - **`TicketId`**: identificador del ticket.
        - **`AccessDate`**: fecha de acceso del ticket. *Formato ISO 8601 (yyyy-MM-dd)*.
        - **`TicketEnclosureId`**: identificador del recinto.
        - **`SessionId`**: identificador de la sesión asignada.
        - **`SessionTime`**: hora de la sesión asignada en caso de haber podido asignar alguna.
        - **`SessionContentId`**: identificador del contenido de sesión.
        - **`SessionContentName`**: nombre del contenido de sesión.
        - **`ResultType`**: atributo que indica el resultado de la auto asignación.

            ??? example "Posibles valores"
                - 0: **Ok**. Auto asignación correcta.
                - 1: **HasNotTicketEnclosure**. El producto no tiene recintos, por lo tanto es un producto sin sesiones.
                - 2: **TicketEnclosureSessionTypeIsNone**. El producto no tiene sesiones en ninguno de sus recintos.
                - 3: **TicketEnclosureDoesNotAcceptAutoAssign**. El producto no tiene recintos con sesiones configuradas como auto asignables.
                - 4: **TicketEnclosureHasNoSessionsAvailable**. No hay sesiones disponibles para el producto y fecha seleccionados.

--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/autoAssignSessionResponseExamples.md"
