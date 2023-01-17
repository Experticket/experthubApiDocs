# Canje de tickets

Con este método del API es posible realizar el canje de tickets.

## Método de acceso

**POST** activity/ticketexchange

## Estructura de la petición

- **`Exchanges`** (``list``): array con los datos de los tickets que queremos canjear.
    - **``Exchange``** (``object``): canjeo que se quiere realizar.
        - **`TicketAccessCode`** (``string``): código de acceso del ticket.
        - **`InternalCode`** (``string``): *opcional*, código que queremos asignar al ticket canjeado.

### Ejemplo de petición

--8<-- "includes/examples/activity/ticketExchangeQueryExamples.md"

## Estructura de la respuesta

--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/ticketExchangeResponseExamples.md"
