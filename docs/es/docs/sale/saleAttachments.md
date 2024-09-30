# Adjuntar documentos a la venta

Este método permite adjuntar documentos a la venta. Por ejemplo documentos acreditativos de discapacidad/familia numerosa o monoparental.

## Método de acceso

**PUT** /Sale

## Estructura de la petición

El Content-Type de la petición debe ser multipart/form-data, incluyendo los siguientes campos:

- **``SaleId``**: (``string``) ``Requerido``. Identificador de la venta.
- **``Attachments``**: (``list[list]``) ``Requerido``. Un array en el que cada elemento es un array de bytes del documento a adjuntar. 

??? tip "Información"
        El identificador de la venta se obtiene en la respuesta de la llamada a [confirmación de la reserva](../ShoppingCart/sale.md). Esta función nos devolverá un listado de ventas con sus identificadores(Id). Ese identificador es el que debemos usar en este campo.
  
### Ejemplo de llamada

??? tip "Examples"

    --8<-- "includes/examples/sale/saleAttachmentsRequest.request.1.md"

## Estructura de la respuesta

    --8<-- "includes/experthubResponseBaseDocumentation.es.md"

### Ejemplo de respuesta

??? tip "Examples"

    --8<-- "includes/examples/sale/saleAttachmentsRequest.response.1.md"
