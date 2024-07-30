            - **`Activity`**: (`object`). Información de la actividad.
                - **`ProductId`**: (`string`). Identificador del producto.
                - **`CombinedProductId`**: (`string`) `Opcional`. Identificador del producto combinado.
                - **`CombinedProductDiscriminator`**: (`byte`) `Opcional`. Indica a qué producto combinado pertenece dentro del array de CombinedProducts.
                - **`AccessCode`**: (`string`) `Opcional`. Código de barras (si corresponde).
                - **`AccessDateTime`**: (`date`) `Requerido`. Fecha de acceso. Formato IS0 8601 (YYYY-MM-DD).
                - **`Quantity`**: (`int`) `Requerido`. Cantidad de productos.
                - **`ProductName`**: (`string`). Nombre del producto.
                - **`ProviderId`**: (`string`). Identificador del proveedor.
                - **`ProviderName`**: (`string`). Nombre del proveedor.
                - **`Price`**: (`decimal`). Indica el precio al que se ha vendido el producto.
                - **`PriceWithoutVat`**: (`decimal`). Indica el precio al que se ha vendido el producto sin impuestos.
                - **`PriceMode`**: (`int`). Tipo de precio:
            
                    ??? example "Posibles valores"
                        --8<-- "includes/enum/priceMode.md"
            
                - **`Status`**: (`int`). Tipo de precio.
            
                    ??? example "Posibles valores"
                        --8<-- "includes/enum/activityStatus.md"
              
                - **`Discount`**: (`decimal`). Descuento total aplicado al producto. Solo aparece si se ha aplicado algún cupón descuento.
                - **`DiscountCoupons`**: (`list`). Cupones descuento aplicados al producto. Solo aparece en caso de que al producto se le haya aplicado algún cupón descuento.
                    - **`DiscountCouponId`**: (`string`). Identificado del cupón descuento.
                    - **`Name`**: (`string`). Nombre del cupón descuento.
                    - **`Description`**: (`string`). Descripción del cupón descuento.
                    - **`Discount`**: (`decimal`). Descuento que ha generado sobre el producto.
                    - **`Code`**: (`string`). Código usado para la aplicación del cupón descuento.
                - **`FinancialRatios`**: (`Objeto`). Conceptos económicos de una venta.
                    - **`ReferenceSalePrice`**: (`Objeto`). Precio de venta de referencia.
                          --8<-- "includes/annex/financialRatios.es.md"
                    - **`Discount`**: (`Objeto`). Descuento comercial.
                          --8<-- "includes/annex/financialRatios.es.md"
                    - **`Commission`**: (`Objeto`). Coste de colaborador.
                          --8<-- "includes/annex/financialRatios.es.md"
                - **`SalePrice`**: (`Objeto`). Precio de venta.
                - **`Tickets`**: (`object`) `Opcional`. Lista con la información del ticket.
                    - **`TicketId`**: (`string`) `Requerido`. Identificador del ticket.
                    - **`SessionId`**: (`string`) `Opcional`. Identificador de la sesión.
                    - **`SessionTime`**: (`date`) `Opcional`. Hora de la sesión.
                    - **`AccessDateTime`**: (`date`) `Requerido`. Construye el mensaje que se sugiere que se muestre respecto a la fecha de acceso en el documento de acceso en función de AccessDateCriteria, AccessDateCriteriaOpenDateSalesDocument, AccessDateTime y AccessEndDateTime.
                    - **`AccessEndDateTime`**: (`date`) `Requerido`. En caso de existir, indica la fecha de fin de validez de acceso del ticket. Formato IS0 8601 (YYYY-MM-DD).
                    - **`SuggestedAccessDateMessage`**: (`string`). Código de barras (si corresponde).
                    - **`AccessCode`**: (`string`) `Opcional`. Código de barras (si corresponde).
                    - **`TicketEnclosureId`**: (`string`). Identificador del recinto del ticket.
                    - **`TicketEnclosureName`**: (`string`). Nombre del recinto del ticket.
                    - **`Questions`**: (`object`) `Opcional`. Identificador del ticket.
                        - **`TicketQuestionId`**: (`string`) `Requerido`. Identificador de la pregunta.
                        - **`Question`**: (`string`). Pregunta.
                - **`CancellationConditions`**: (`object`). Indica las políticas de cancelación que se aplican al cancelar la venta de este producto.
                    - **`IsRefundable`**: (`boolean`). Indica si el cliente puede cancelar gratis en algún momento.
                    - **`Rules`**: (`list`). Reglas que se aplican al efectuar la cancelación.
                        - **`Percentage`**: (`decimal`). Porcentaje de penalización sobre el precio de la entrada.
                        - **`Amount`**: (`decimal`). Importe total de la cancelación.
                        - **`FromInclusiveDateTime`**: (`date`). Fecha desde la que se aplica la penalización (incluida). Formato IS0 8601 (YYYY-MM-DD).
                        - **`ToExclusiveDateTime`**: (`date`). Fecha hasta la que se aplica la penalización (excluida). Formato IS0 8601 (YYYY-MM-DD).
                        - **`HoursInAdvanceOfAccess`**: (`int`). Indica la cantidad de horas de antelación con respecto a la fecha de acceso a partir de las cuales se aplicará la penalización de precio indicada en Amount.
