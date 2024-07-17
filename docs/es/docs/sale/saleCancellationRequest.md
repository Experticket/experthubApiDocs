# Solicitud de cancelación

Este método permite crear una solicitud de cancelación para una venta.

## Método de acceso

**POST** /salecancellationrequest

## Estructura de la petición

- **`PartnerSaleId`**: (``string``) ``Requerido``. Identificador del colaborador.
  - **`Reason`**: (``int``) ``Opcional``. Motivos por los cuales quiere solicitarse la cancelación:
      
    ??? example "Posibles valores"
        --8<-- "includes/enum/cancellationRequestReason.md"

- **`ReasonComments`**: (``string``). ``Opcional``. Comentarios de la solicitud de cancelación de una transacción.

### Ejemplo de llamada

??? tip "Ejemplos"

    --8<-- "includes/examples/sale/createSaleCancellationRequest.request.1.md"

## Estructura de la respuesta

- **`Timestamp`**: (``dateTime``). Instante de tiempo en el que se procesó la petición. Formato ISO 8601 (yyyy-MM-ddThh\:mm\:ss.fffffff).
- **`Success`**: (``boolean``). Valor que indica si la llamada ha sido procesada correctamente o no.
- **`Errors`**: (`list`). Array de errores.
  - **`Error`**: (`object`).
    - **`ErrorMessage`**: (`string`). Mensaje de error explicando por qué la petición no ha sido correcta. En caso que haya sido correcta, devolverá `#!csharp null`.
    - **`ErrorCode`**: (`int`). Código que identifica al error.

--8<-- "includes/experthubResponseBaseDocumentation.es.md"

### Ejemplo de respuesta

??? tip "Examples"

    --8<-- "includes/examples/sale/createSaleCancellationRequest.response.1.md"