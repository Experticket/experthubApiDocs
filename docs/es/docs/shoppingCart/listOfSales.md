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
    - **`PartnerSaleId`**: (`string`). Identificador del colaborador.    
    - **`Activities`**: (`list`). Listado de actividades.
        - [Anexo: Actividad](../annex/activity.es.md)       
    - **`Accommodations`**: (`list`). Listado de alojamientos incluidos en la venta.
        - [Anexo: Alojamiento](../annex/accommodation.es.md)    
    - **`CombinedProducts`**: (`list`). Listado de productos combinados de las actividades incluidos en la venta.
        - [Anexo: Producto Combinado](../annex/combinedProduct.es.md)
    - **`Client`**: (`object`). Datos del cliente de la venta.
        - [Anexo: Cliente](../annex/client.es.md)
    - **`TotalPrice`**: (`decimal`). Indica el precio total de la venta.
    - **`TotalPriceWithoutVat`**: (`decimal`). Indica el precio total de la venta sin impuestos.
    - **`TotalDiscount`**: (`decimal`). Descuento total aplicado sobre la venta. Solo aparece si se ha aplicado algún cupón descuento.
    - **`InsurancePolicyAmount`**: (`decimal`). Indica el precio total del seguro de reembolso.
    - **`InsurancePolicyAmountWithoutTaxes`**: (`decimal`). Indica el precio total del seguro de reembolso sin impuestos.
    
- **`PageNumber`**: (`int`). Indica la página solicitada.
- **`HasPreviousPage`**: (`boolean`). Indica si hay una página previa a la solicitada.
- **`HasNextPage`**: (`boolean`). Indica si hay una siguiente página.
- **`IsFirstPage`**: (`boolean`). Indica si la página solicitada corresponde a la primera página.

--8<-- "includes/experthubResponseBaseDocumentation.es.md"

### Ejemplo de respuesta

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/listOfSales.response.1.md"
