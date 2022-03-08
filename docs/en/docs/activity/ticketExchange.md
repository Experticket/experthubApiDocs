# Ticket exchange

With this API method it is possible to exchange tickets.

## Access method

**POST** activity/ticketexchange

## Request data structure

- **`Exchanges`**: array with the data of the tickets that we want to exchange.
    - **`TicketAccessCode`**: ticket access code.
    - **`InternalCode`**: *optional*, code that we want to assign to the exchanged ticket.

### Request example

--8<-- "includes/examples/activity/ticketExchangeQueryExamples.md"

## Response structure

--8<-- "includes/responseBaseDocumentation.es.md"

### Response example

--8<-- "includes/examples/activity/ticketExchangeResponseExamples.md"
