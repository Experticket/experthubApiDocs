# Listado de ventas

Este método permite obtener el listado de ventas.

## Método de acceso

**GET** /Sale

## Estructura de la petición

Requiere pasarle, como parámetro de la url (query string), los siguientes parámetros:
Filtros disponibles para la obtención del listado de ventas. Estos filtros se envían como parámetros en la URL (`query string`). Filtros disponibles:

| Parámetro | Descripción |
| --- | --- |
|``PartnerSaleId`` | ``Obligatorio`` Identificador del colaborador |
|``FromTransactionDateTime`` | ``Opcional`` Fecha inicial de creación de la transacción. Formato IS0 8601 (YYYY-MM-DD) |
|``ToTransactionDateTime`` | ``Opcional`` Fecha final de creación de la transacción. Formato IS0 8601 (YYYY-MM-DD) |
|``FromAccessDateTime`` | ``Opcional`` Fecha inicial de acceso. Formato IS0 8601 (YYYY-MM-DD) |
|``ToAccessDateTime`` | ``Opcional`` Fecha final de acceso. Formato IS0 8601 (YYYY-MM-DD) |
|``ToAccessDateTime`` | ``Opcional`` Fecha final de acceso. Formato IS0 8601 (YYYY-MM-DD) |
|``ClientName`` | ``Opcional`` Nombre del cliente |
|``ClientEmail`` | ``Opcional`` Email del cliente |
|``ClientPhone`` | ``Opcional`` Teléfono del cliente |
|``ClientDocumentIdentifier`` | ``Opcional`` Documento de identidad del cliente |
|``Page`` | ``Opcional`` Número de página a obtener. Valor por defecto `1` |
|``PageSize`` | ``Opcional`` Número de resultados a obtener|


### Ejemplos

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/listOfSales.request.1.md"

## Estructura de la respuesta

- **`Success`**: (``boolean``). Indica si la llamada ha sido procesada satisfactoriamente.
- **`Sales`**: (``list``). Listado de ventas.
- **`PageNumber`**: (``int``). Indica la paágina solicitada.
- **`HasPreviousPage`**: (``boolean``). Indica si hay una página previa a la solicitada.
- **`HasNextPage`**: (``boolean``). Indica si hay una siguiente página.
- **`IsFirstPage`**: (``boolean``). Indica si la página solicitada corresopnde a la primera página

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/sale.response.1.md"