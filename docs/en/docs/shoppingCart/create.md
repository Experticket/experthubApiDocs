# Create a cart

This method allows us to create a shopping cart (from now on, **cart**).

The cart is a container for products (activities, accommodations, and/or packages). It can contain 0 to N products.

The cart itself does not expire. However, the products added to it do expire.

## Access method

**POST** /ShoppingCart/Create

## Request structure

There is no request body.

## Response structure

- **`Id`**: (`string`). Cart identifier.

--8<-- "includes/experthubResponseBaseDocumentation.en.md"

### Response example

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/create.response.1.md"
