# Get documentation

This method allows us to obtain the documentation for a confirmed sale in the specified languages.

## Access method

**GET** /ShoppingCart/Documentation

## Request structure

The following parameters must be passed as URL query string parameters:

- **`ShoppingCartId`**: (`string`). `Required`. Shopping cart identifier.
- **`Language`**: (`list`). `Optional`. Indicates the language in which the documentation will be downloaded.

!!! warning ""
    If the `Language` field is not specified, the documentation will be downloaded in the partner's default language. If more than one language is specified by repeating the query parameter as many times as needed, a single PDF will be downloaded containing the documentation in all the requested languages.

### Request example

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/documentation.request.1.md"

## Response structure

Returns a byte array containing the PDF (`Byte[]`).
