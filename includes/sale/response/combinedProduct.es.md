- **`CombinedProductId`**: (`string`). Identificador del producto combinado.
- **`CombinedProductDiscriminator`**: (`string`). Relación existente entre producto(Array de Products) y producto
  combinado.
- **`Price`**: (`decimal`). Precio de cada producto combinado.
- **`PriceWithoutVat`**: (`decimal`). Precio de cada producto combinado sin impuestos.
- **`CancellationConditions`**: (`object`). Indica las políticas de cancelación que se aplican al cancelar la venta
  de este producto.
    - **`IsRefundable`**: (`boolean`). Indica si el cliente puede cancelar gratis en algún momento.
    - **`Rules`**: (`list`). Reglas que se aplican al efectuar la cancelación.
        - **`Percentage`**: (`decimal`). Porcentaje de penalización sobre el precio de la entrada.
        - **`Amount`**: (`decimal`). Importe total de la cancelación.
        - **`FromInclusiveDateTime`**: (`date`). Fecha desde la que se aplica la penalización (incluida). Formato IS0 8601 (YYYY-MM-DD).
        - **`ToExclusiveDateTime`**: (`date`). Fecha hasta la que se aplica la penalización (excluida). Formato IS0 8601 (YYYY-MM-DD).
        - **`HoursInAdvanceOfAccess`**: (`int`). Indica la cantidad de horas de antelación con respecto a la fecha de acceso a partir de las cuales se aplicará la penalización de precio indicada en Amount.
