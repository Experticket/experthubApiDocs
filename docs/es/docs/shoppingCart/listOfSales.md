# Listado de ventas

Este método permite obtener el listado de ventas.

## Método de acceso

**GET** /Sale

## Estructura de la petición

Requiere pasarle, como parámetro de la url (query string), los siguientes parámetros:
Filtros disponibles para la obtención del listado de ventas. Estos filtros se envían como parámetros en la URL (`query string`). Filtros disponibles:

- **`PartnerSaleId`**: (``string``).  ``Opcional`` Identificador del colaborador.
- **`FromTransactionDateTime`**: (``date``).  ``Opcional`` Fecha inicial de creación de la transacción. Formato IS0 8601 (YYYY-MM-DD).
- **`ToTransactionDateTime`**: (``date``).  ``Opcional`` Fecha final de creación de la transacción. Formato IS0 8601 (YYYY-MM-DD).
- **`FromAccessDateTime`**: (``date``).  ``Opcional`` Fecha inicial de acceso. Formato IS0 8601 (YYYY-MM-DD).
- **`ToAccessDateTime`**: (``date``).  ``Opcional`` Fecha final de acceso. Formato IS0 8601 (YYYY-MM-DD).
- **`ClientName`**: (``string``).  ``Opcional`` Nombre del cliente.
- **`ClientEmail`**: (``string``).  ``Opcional`` Email del cliente.
- **`ClientPhone`**: (``string``).  ``Opcional`` Teléfono del cliente.
- **`ClientDocumentIdentifier`**: (``string``).  ``Opcional`` Documento de identidad del cliente.
- **`Page`**: (``int``).  ``Opcional`` Número de página a obtener. Valor por defecto `1`.
- **`PageSize`**: (``int``).  ``Opcional`` Número de resultados a obtener.
  
### Ejemplo de llamada

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/listOfSales.request.1.md"

## Estructura de la respuesta

- **`Sales`**: (`list`). Listado de ventas.
    - **`Activities`**: (`list`). Listado de actividades.
        --8<-- "includes/sale/response/activity.es.md"
    - **`Accommodations`**: (`list`). Listado de productos combinados de las actividades incluidos en la venta.
        --8<-- "includes/sale/response/accommodation.es.md"
    - **`CombinedProducts`**: (`list`). Listado de productos combinados de las actividades incluidos en la venta.
        - **`CombinedProductId`**: (`string`). Identificador del producto combinado. 
        - **`CombinedProductDiscriminator`**: (`string`). Relación existente entre producto(Array de Products) y producto combinado. 
        - **`Price`**: (`decimal`). Precio de cada producto combinado. 
        - **`PriceWithoutVat`**: (`decimal`). Precio de cada producto combinado sin impuestos. 
        - **`CancellationConditions`**: (`object`). Indica las políticas de cancelación que se aplican al cancelar la venta de este producto.
            - **`IsRefundable`**: (`boolean`). Indica si el cliente puede cancelar gratis en algún momento.
            - **`Rules`**: (`list`). Reglas que se aplican al efectuar la cancelación.
                - **`Percentage`**: (`decimal`). Porcentaje de penalización sobre el precio de la entrada.
                - **`Amount`**: (`decimal`). Importe total de la cancelación.
                - **`FromInclusiveDateTime`**: (`date`). Fecha desde la que se aplica la penalización (incluida). Formato IS0 8601 (YYYY-MM-DD).
                - **`ToExclusiveDateTime`**: (`date`). Fecha hasta la que se aplica la penalización (excluida). Formato IS0 8601 (YYYY-MM-DD).
                - **`HoursInAdvanceOfAccess`**: (`int`). Indica la cantidad de horas de antelación con respecto a la fecha de acceso a partir de las cuales se aplicará la penalización de precio indicada en Amount. 
- **`PageNumber`**: (`int`). Indica la página solicitada.
- **`HasPreviousPage`**: (`boolean`). Indica si hay una página previa a la solicitada.
- **`HasNextPage`**: (`boolean`). Indica si hay una siguiente página.
- **`IsFirstPage`**: (`boolean`). Indica si la página solicitada corresponde a la primera página.

--8<-- "includes/experthubResponseBaseDocumentation.es.md"

### Ejemplo de respuesta

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/sale.response.1.md"
