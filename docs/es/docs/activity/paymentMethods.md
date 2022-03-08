# Métodos de pago

Este es un paso intermedio que debemos realizar antes de confirmar el carrito. Véase el campo ``PartnerSettings`` en el [catálogo](catalog.md).

!!! success ""
    Si **``PaymentType``** en el catálogo indica que nuestra forma de pago es diferente de débito está llamada es irrelevante para nosotros.
!!! warning ""
    Si **``PaymentType``** en el catálogo indica que nuestra forma de pago al distribuidor es débito deberemos hacer uso de está llamada.

## Método de acceso

**GET** activity/paymentmethods

## Estructura de datos de la petición

- **`ReservationId`**: identificador de la reserva obtenido al confirmar el carrito.

### Ejemplo de petición

--8<-- "includes/examples/activity/paymentMethodsQueryExamples.md"

## Estructura de datos de la respuesta

- **`PaymentMethods`**: array de métodos de pago.
    - **``Type``**: identificador del tipo de método de pago.
    - **``Name``**: nombre del método de pago.
    - **``EnableSendByEmails``**: indica si podemos usar este método de pago para mandar automaticamente un enlace de pago al cliente final vía email.
- **`Success`**: valor de verdad, `#!csharp true/false` que indica si la llamada ha sido procesada correctamente o no.
- **`Timestamp`**: instante de tiempo en el que se procesó la petición. *Formato ISO 8601 (yyyy-MM-ddThh:mm:ss.fffffff)*.
- **`ErrorMessage`**: mensaje de error explicando por qué la petición no ha sido correcta. En caso que haya sido correcta, devolverá `#!csharp null`.

### Ejemplo de respuesta

--8<-- "includes/examples/activity/paymentMethodsResponseExamples.md"
