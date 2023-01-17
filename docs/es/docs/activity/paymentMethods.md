# Métodos de pago

Este es un paso intermedio que debemos realizar antes de confirmar el carrito. Véase el campo ``PartnerSettings`` en el [catálogo](catalog.md).

!!! success ""
    Si **``PaymentType``** en el catálogo indica que nuestra forma de pago es diferente de débito está llamada es irrelevante para nosotros.
!!! warning ""
    Si **``PaymentType``** en el catálogo indica que nuestra forma de pago al distribuidor es débito deberemos hacer uso de está llamada.

## Método de acceso

**GET** activity/paymentmethods

## Estructura de la petición

- **`ReservationId`**: (``string``). Identificador de la reserva obtenido al confirmar el carrito.

### Ejemplo de petición

--8<-- "includes/examples/activity/paymentMethodsQueryExamples.md"

## Estructura de la respuesta

- **`PaymentMethods`**: (``list``). Array de métodos de pago.
    - **``Type``**: (``byte``). Identificador del tipo de método de pago.
    - **``Name``**: (``string``). Nombre del método de pago.
    - **``EnableSendByEmails``**: (``boolean``). Indica si podemos usar este método de pago para mandar automaticamente un enlace de pago al cliente final vía email.
--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/paymentMethodsResponseExamples.md"
