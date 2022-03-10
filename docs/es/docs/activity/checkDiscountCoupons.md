# Comprobar cupones descuento

A través de esta llamda se comprueba si se pueden aplicar uno o más cupones de descuento, y los efectos que producen en la venta.

## Método de acceso

**POST** activity/discountcouponscheck

## Estructura de la petición

- **`DiscountCoupons`**: resumen de resultados de cupones de descuento.
    - **`Id`**: identificador de cupón de descuento.
    - **`Code`**: código de cupón de descuento.
    - **`Name`**: nombre del cupón de descuento.
    - **`Description`**: descripción del cupón de descuento.
    - **`IsValid`**: `true` si el cupón es válido, de lo contrario `false`.
- **`Sale`**: información de venta.
    - **`Products`**: lista de productos.
        - **`Id`**: identificador único del producto.
        - **`ProductId`**: identificador de producto obtenido por una llamada previa al catálogo.
        - **`Price`**: precio final, después de aplicar los descuentos.
        - **`Discounts`**: descuento total aplicado.
        - **`PriceWithoutDiscounts`**: precio del producto antes de aplicar los descuentos.
        - **`AppliedCoupons`**: cupones aplicados.
            - **`Id`**: identificador de cupón de descuento.
            - **`Code`**: código de cupón de descuento.
            - **`Discount`**: descuento generado por el cupón.
            - **`AppliesTo`**: indica sobre qué precio se aplica el descuento.

                ??? example "Valores posibles"
                    - 0: indica que el descuento se ha aplicado al precio original del producto.
                    - 1: indica que el descuento se ha aplicado al precio actual del producto (precio original menos descuentos generados por otros cupones de descuento).

            - **`Name`**: nombre del cupón de descuento.
            - **`Description`**: descripción del cupón de descuento.
            - **`Order`**: orden de solicitud de cupón de descuento.
            - **`PriceModifierType`**: indica el tipo de descuento.

                ??? example "Valores posibles"
                    - 1: descuento porcentual.
                    - 3: descuento de valor absoluto.

            - **`PriceModifieralue`**: importe del descuento aplicado. Su interpretación depende del valor del atributo `PriceModifierType`.

### Ejemplo de petición

--8<-- "includes/examples/activity/checkDiscountCouponsQueryExamples.md"

## Estructura de la respuesta

- **`ShippingCosts`**: gastos de envío.
- **`DeliveryDays`**: estimación de los días necesarios para que los productos lleguen a su destino.
--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/checkDiscountCouponsResponseExamples.md"
