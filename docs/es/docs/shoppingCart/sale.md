# Confirmación de la reserva

Este método confirma la reserva realizada previamente en nuestros sistemas.

## Método de acceso

**POST** /ShoppingCart/Sale

## Estructura de la petición

- **``ShoppingCartId``**: (``string``) ``Requerido``. Identificador del carrito.
- **``PartnerSaleId``**: (``string``) ``Requerido``. Identificador del colaborador.
- **``DiscountCouponCodes``**: (``list``) ``Requerido``. Identificador del colaborador.
- **``Client``**: (``object``) ``Opcional``. Información del cliente. Si la venta contiene hoteles, esta propiedad es obligatoria. Si únicamente contiene actividades, este parámetro dependerá de la configuración que se haya acordado con el colaborador.
    - **``FullName``**: (``string``) ``Requerido``. Nombre.
    - **``Surname``**: (``string``) ``Requerido``. Apellidos.
    - **``DocumentIdentifier``**: (``string``) ``Requerido``. Documento de identidad.
    - **``PhoneNumber``**: (``string``) ``Requerido``. Teléfono.
    - **``Email``**: (``string``) ``Requerido``. Correo electrónico.
- **``PaymentMethod``**: (``string``) ``Opcional``. Información del método de pago. Únicamente habrá que rellenarlo en caso que el colaborador tenga un contrato a débito.
    - **``PaymentMethodType``**: (``int``) ``Requerido``. Identificador del método de pago.
    - **``ReturnUrlOk``**: (``string``) ``Requerido``. Url en la cual se notificará que el cobro ha ido correctamente.
    - **``ReturnUrlKo``**: (``string``) ``Requerido``. Url en la cual se notificará que el cobro ha sido fallido.
    - **``SendByEmail``**: (``boolean``) ``Requerido``. tbd.


### Ejemplos

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/sale.request.1.md"

## Estructura de la respuesta

- **`Success`**: (``boolean``). Indica si la llamada ha sido procesada satisfactoriamente.
- **`ExperticketSales`**: (``list``). Listado de ventas asociadas en Experticket.
    - **`ExperticketSale`**: (``object``). Información de la venta.
        - **`Id`**: (``string``). tbd

??? tip "Examples"

    --8<-- "includes/examples/shoppingCart/sale.response.1.md"