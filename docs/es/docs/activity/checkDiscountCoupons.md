# Comprobar cupones descuento

A través de esta llamada se comprueba si se pueden aplicar uno o más cupones de descuento, y los efectos que producen en la venta.

## Método de acceso

**POST** activity/discountcouponcheck

## Estructura de la petición

- **``DiscountCouponCodes``**: (``list``). Array de cupones descuento a comprobar.
    - **``(string)``**: Identificador del cupón descuento.
- **``Sale``**: (``object``). Información de la venta.
    - **``Products``**: (``list``). Array de productos.
        - **``Id``**: (``string``). Identificador único del producto generado por el colaborador.
        - **``ProductId``**: (``string``). Identificador del producto.
        - **``Price``**: (``decimal``). Precio del producto.
        - **``AccessDate``**: (``date``) ``Opcional``. Fecha de acceso del produto.

### Ejemplo de petición

--8<-- "includes/examples/activity/checkDiscountCouponsQueryExamples.md"

## Estructura de la respuesta

- **`DiscountCoupons`**: (``list``). Resumen de resultados de cupones de descuento.
    - **`Id`**: (``string``). Identificador de cupón de descuento.
    - **`Code`**: (``string``). Código de cupón de descuento.
    - **`Name`**: (``string``). Nombre del cupón de descuento.
    - **`Description`**: (``string``). Descripción del cupón de descuento.
    - **`IsValid`**: (``boolean``). `true` si el cupón es válido, de lo contrario `false`.
- **`Sale`**: (``object``). Información de venta.
    - **`Products`**: (``list``). Lista de productos.
        - **`Id`**: (``string``). Identificador único del producto generado por el colaborador, sirve para identificar a que producto concreto aplica el descuento en caso de tener varios productos iguales en el carrito.
        - **`ProductId`**: (``string``). Identificador de producto.
        - **`Price`**: (``decimal``). Precio final, después de aplicar los descuentos.
        - **`Discounts`**: (``decimal``). Descuento total aplicado.
        - **`PriceWithoutDiscounts`**: (``decimal``). Precio del producto antes de aplicar los descuentos.
        - **`AppliedCoupons`**: (``lista``). Cupones aplicados.
            - **`Id`**: (``string``). Identificador de cupón de descuento.
            - **`Code`**: (``string``). Código de cupón de descuento.
            - **`Discount`**: (``decimal``). Descuento generado por el cupón.
            - **`AppliesTo`**: (``byte``). Indica sobre qué precio se aplica el descuento.

                ??? example "Valores posibles"
                    - 0: indica que el descuento se ha aplicado al precio original del producto.
                    - 1: indica que el descuento se ha aplicado al precio actual del producto (precio original menos descuentos generados por otros cupones de descuento).

            - **`Name`**: (``string``). Nombre del cupón de descuento.
            - **`Description`**: (``string``). Descripción del cupón de descuento.
            - **`Order`**: (``int``). Orden de solicitud de cupón de descuento.
            - **`PriceModifierType`**: (``byte``). Indica el tipo de descuento.

                ??? example "Valores posibles"
                    - 1: descuento porcentual.
                    - 3: descuento de valor absoluto.

            - **`PriceModifierValue`**: (``byte``). Importe del descuento aplicado. Su interpretación depende del valor del atributo `PriceModifierType`.

--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/checkDiscountCouponsResponseExamples.md"
