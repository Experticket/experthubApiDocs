# Ticket exchange

With this API method it is possible to exchange tickets.

## Access method

**POST** activity/ticketexchange

## Request structure

- **`Exchanges`** (``list``): array with the data of the tickets that we want to exchange.
    - **``Exchange``** (``object``): exchange to be performed.
        - **`TicketAccessCode`** (``string``): ticket access code.
        - **`InternalCode`** (``string``): *optional*, code that we want to assign to the exchanged ticket.

### Request example

--8<-- "includes/examples/activity/ticketExchangeQueryExamples.md"

## Response structure

--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/activity/ticketExchangeResponseExamples.md"
