# Solicitud de cancelación

Este método permite crear una solicitud de cancelación para una venta.

## Método de acceso

**POST** /salecancellationrequest

## Estructura de la petición

- **`PartnerSaleId`**: (``string``) ``Requerido``. Identificador del colaborador.
  - **`Reason`**: (``int``) ``Opcional``. Motivos por los cuales quiere solicitarse la cancelación:
      
    ??? example "Posibles valores"
        --8<-- "includes/enum/cancellationRequestStatus.md"

- **`ReasonComments`**: (``string``). ``Opcional``. Comentarios de la solicitud de cancelación de una transacción.

### Ejemplo de llamada

--8<-- "includes/examples/sale/createSaleCancellationRequest.request.1.md"

## Estructura de la respuesta

- **`Timestamp`**: (``dateTime``). Instante de tiempo en el que se procesó la petición. Formato ISO 8601 (yyyy-MM-ddThh\:mm\:ss.fffffff).

--8<-- "includes/experthubResponseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/sale/createSaleCancellationRequest.response.1.md"
