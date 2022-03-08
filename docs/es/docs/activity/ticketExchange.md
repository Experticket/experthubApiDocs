# Canje de tickets

Con este método del API es posible realizar el canje de tickets.

## Método de acceso

**POST** activity/ticketexchange

## Estructura de la petición

- **`Exchanges`**: array con los datos de los tickets que queremos canjear.
    - **`TicketAccessCode`**: código de acceso del ticket.
    - **`InternalCode`**: *opcional*, código que queremos asignar al ticket canjeado.

### Ejemplo de petición

--8<-- "includes/examples/activity/ticketExchangesQueryExamples.md"

## Estructura de la respuesta

--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/ticketExchangesResponseExamples.md"
