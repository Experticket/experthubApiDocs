# Cancel the reservation

This method removes the reservation that has already been created and invalidates the cart.

## Access method

**POST** /ShoppingCart/CancelConfirm

## Request structure

- **`ShoppingCartId`**: (`string`) `Required`. Cart identifier.

### Request example

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/cancelConfirm.request.1.md"

## Response structure

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response example

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/cancelConfirm.response.1.md"
