# Remove an item from the cart

This method allows an existing item to be removed from the cart. To do so, it is necessary to use the identifier (**`Id`**) shown in the response of the [**`Add`**](./add.md#response-structure) method.

## Access method

**POST** /ShoppingCart/Remove

## Request structure

- **`ShoppingCartId`**: (`string`) `Required`. Cart identifier.
- **`ShoppingCartItemIdsToRemove`**: (`list`) `Required`. List of identifiers to remove.
    - **`(string)`**: `Required`. Identifier to remove. This identifier is shown in the response of the [**`Add`**](./add.md#response-structure) method.

### Request example

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/remove.request.1.md"

## Response structure

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response example

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/remove.response.1.md"
