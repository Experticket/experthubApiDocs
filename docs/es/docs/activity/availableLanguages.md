# Idiomas disponibles para los documentos de la venta

Con este método del API se obtienen los idiomas en los que está disponible, entre otros, la documentación de las transacciones o el catálogo. Los **``Code``** de cada **``Languages``** que devuelve son los posibles valores que se pueden utilizar en las llamadas [Documentación](../shoppingCart/documentation.md) o [Catálogo](catalog.md).

## Método de acceso

**GET** /activity/availablelanguages

## Estructura de la respuesta

- **`Languages`**: (``list``). Array de objetos que contiene cada uno de los idiomas en los que la documentación está disponible.
    - **`Code`**: (``string``). Código del idioma.
    - **`EnglishName`**: (``string``). Nombre del idioma en inglés.
    - **`NativeName`**: (``string``). Nombre del idioma en su lengua original.
--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/availableLanguagesResponseExamples.md"
