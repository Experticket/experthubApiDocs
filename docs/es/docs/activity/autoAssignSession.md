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

- **`LanguageCode`**: (``string``). Define el idioma en que se mostrarán los textos. *Formato ISO 639-1*.
- **`Products`**: (``list``). Array de productos para los que se quieren comprobar las sesiones.
    - **`ProductId`**: (``string``). Identificador del producto.
    - **`Quantity`**: (``int``). Cantidad del producto.
    - **`AccessDate`**: (``date``). Fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **`Tickets`**: (``list``). Array de tickets para los que queremos comprobar la auto asignación.
        - **`TicketId`**: (``string``). Identificador del ticket.
        - **`AccessDate`**: (``date``) ``Opcional``.  si se indica, tiene preferencia sobre la fecha indicada a nivel de producto. *Formato ISO 8601 (yyyy-MM-dd)*.

### Ejemplo de petición

--8<-- "includes/examples/activity/autoAssignSessionQueryExamples.md"

## Estructura de la respuesta

- **`Products`**: (``list``). Array que contiene los productos solicitados.
    - **`ProductId`**: (``string``). Identificador del producto.
    - **`AccessDate`**: (``date``). Fecha de acceso del producto. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **`HasTicketEnclosures`**: (``boolean``). Booleano que indica si el producto tiene recintos.
    - **`Tickets`**: (``list``). Array de los tickets solicitados del producto.
        - **`TicketId`**: (``string``). Identificador del ticket.
        - **`AccessDate`**: (``date``). Fecha de acceso del ticket. *Formato ISO 8601 (yyyy-MM-dd)*.
        - **`TicketEnclosureId`**: (``string``). Identificador del recinto.
        - **`SessionId`**: (``string``). Identificador de la sesión asignada.
        - **`SessionTime`**: (``date``). Hora de la sesión asignada en caso de haber podido asignar alguna.
        - **`SessionContentId`**: (``string``). Identificador del contenido de sesión.
        - **`SessionContentName`**: (``string``). Nombre del contenido de sesión.
        - **`SessionStartTimeType`**: (``int``). Identificador numérico que indica el tipo de inicio de acceso de la sesión.
            - **`0`**: (``int``): Acceso a la hora indicada.
            - **`1`**: (``int``): Acceso a partir de la hora indicada.
        - **`ResultType`**: (``byte``). Atributo que indica el resultado de la auto asignación.

            ??? example "Posibles valores"
                - 0: **Ok**. Auto asignación correcta.
                - 1: **HasNotTicketEnclosure**. El producto no tiene recintos, por lo tanto es un producto sin sesiones.
                - 2: **TicketEnclosureSessionTypeIsNone**. El producto no tiene sesiones en ninguno de sus recintos.
                - 3: **TicketEnclosureDoesNotAcceptAutoAssign**. El producto no tiene recintos con sesiones configuradas como auto asignables.
                - 4: **TicketEnclosureHasNoSessionsAvailable**. No hay sesiones disponibles para el producto y fecha seleccionados.

--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/autoAssignSessionResponseExamples.md"
