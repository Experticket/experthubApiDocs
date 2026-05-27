# Available languages for sale documents

This API method returns the languages in which transaction documentation, the catalog, and other resources are available. The **`Code`** values returned in **`Languages`** are the valid values that can be used in the [Documentation](../shoppingCart/documentation.md) or [Catalog](catalog.md) calls.

## Access method

**GET** /activity/availablelanguages

## Response structure

- **`Languages`**: (`list`). Array of objects containing each language in which the documentation is available.
    - **`Code`**: (`string`). Language code.
    - **`EnglishName`**: (`string`). Language name in English.
    - **`NativeName`**: (`string`). Language name in its native language.
--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/activity/availableLanguagesResponseExamples.md"
