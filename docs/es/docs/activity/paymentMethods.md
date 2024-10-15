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
  - **`Id`**: (``string``). Identificador del método de pago.
  - **`Type`**: (``byte``). Tipo de método de pago.
  - **`Name`**: (``string``). Nombre del método de pago.
  - **`CommercialName`**: (``string``) ``Opcional``. Nombre comercial del método de pago.
  - **`EnableSendByEmail`**: (``boolean``) ``Opcional``. Indica si es posible utilizar este método de cobro para el envío automático de enlace de cobro por correo.
  - **`Fields`**: (``list``). Array de campos rellenables asociados al método de pago. Estos campos se pueden especificar en el momento de crear una transacción.
    - **`Id`**: (``string``). Identificador del campo.
    - **`Name`**: (``string``). Nombre del campo.
    - **`IsRequired`**: (``boolean``). Indica si se obligatorio rellenar el campo. 
    - **`RegexValidation`**: (``string``) ``Opcional``. Expresión regular que se debe cumplir al rellenar el valor del campo.
    - **`RegexValidationErrorMessage`**: (``string``) ``Opcional``. Mensaje de error a mostrar al usuario en caso de que no se cumpla la expresión regular.
    - **`DefaultValue`**: (``string``) ``Opcional``. Valor por defecto del campo que se debe mostrar al usuario.
    - **`DataType`**: (``byte``). Indica el tipo de datos que debe tener el valor del campo.

        ??? example "Posibles valores"
            - 0: Texto
            - 1: Númerico
            - 2: Fecha
            - 3: Booleano
--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/paymentMethodsResponseExamples.md"
