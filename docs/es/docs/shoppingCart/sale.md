# Confirmación de la reserva

Este método confirma la reserva realizada previamente en nuestros sistemas.

## Método de acceso

**POST** /ShoppingCart/Sale

## Estructura de la petición

- **``ShoppingCartId``**: (``string``) ``Requerido``. Identificador del carrito.
- **``PartnerSaleId``**: (``string``) ``Requerido``. Identificador del colaborador.
- **``InsurancePolicyId``**: (``string``) ``Opcional``. Identificador de la póliza de seguro de reembolso.

    ??? tip "Información"
        Este identificador se obtiene al hacer la llamada para [comprobar pólizas disponibles](../activity/checkInsurancePolicies.md). Esta función nos devolverá un listado de polizas disponibles con sus identificadores(Id). Ese identificador es el que debemos usar en este campo.

- **``DiscountCouponCodes``**: (``list``) ``Opcional``. Listado de cupones (descuentos/promociones) que emite el recinto mediante esta plataforma.
    - **``(string)``**: (``list``) ``Requerido``. Código del cupón.
- **``Client``**: (``object``) ``Opcional``. Información del cliente. Si la venta contiene hoteles, esta propiedad es obligatoria. Si únicamente contiene actividades, este parámetro dependerá de la configuración que se haya acordado con el colaborador.
    - **``FullName``**: (``string``) ``Requerido``. Nombre.
    - **``Surname``**: (``string``) ``Requerido``. Apellidos.
    - **``DocumentIdentifier``**: (``string``) ``Requerido``. Documento de identidad.
    - **``PhoneNumber``**: (``string``) ``Requerido``. Teléfono.
    - **``Email``**: (``string``) ``Requerido``. Correo electrónico.
- **``PaymentMethod``**: (``string``) ``Opcional``. Información del método de pago. Únicamente habrá que rellenarlo en caso de que el colaborador tenga un contrato a débito.
    - **``PaymentMethodType``**: (``int``) ``Requerido``. Identificador del método de pago.
    - **``ReturnUrlOk``**: (``string``) ``Requerido``. Url en la cual se notificará que el cobro ha ido correctamente.
    - **``ReturnUrlKo``**: (``string``) ``Requerido``. Url en la cual se notificará que el cobro ha sido fallido.
    - **``SendByEmail``**: (``boolean``) ``Requerido``. Indica que queremos hacerle llegar un enlace por email al cliente para que realice el pago, en caso de tener la opción de hacer llegar un enlace de pago al cliente por email disponible. Ver [PaymentMethods.PaymentMethod.EnableSendByEmail](./confirm.md#estructura-de-la-respuesta)

### Ejemplo de llamada

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/sale.request.1.md"

## Estructura de la respuesta

- **`PaymentRedirectUrl`**: (``string``). En caso de colaborador con pago a débito, esta propiedad indica la URL donde habrá que redirigir al cliente para hacer el pago.
- **`ExperticketSales`**: (``list``). Listado de ventas asociadas.
    - **`ExperticketSale`**: (``object``). Información de la venta.
        - **`Id`**: (``string``). Identificador de la venta.
            - **`FinancialRatios`**: (``Objeto``). Conceptos económicos de una venta.
                - **`ReferenceSalePrice`**: (``Objeto``). Precio de venta de referencia.
                    --8<-- "includes/annex/financialRatios.es.md"
                - **`Discount`**: (``Objeto``). Descuento comercial.
                    --8<-- "includes/annex/financialRatios.es.md"
                - **`Commission`**: (``Objeto``). Coste de colaborador.
                    --8<-- "includes/annex/financialRatios.es.md"
                - **`SalePrice`**: (``Objeto``). Precio de venta.
                    --8<-- "includes/annex/financialRatios.es.md"

--8<-- "includes/experthubResponseBaseDocumentation.es.md"

### Ejemplo de respuesta

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/sale.response.1.md"
