# Listado de solicitudes de cancelación

Este método permite crear una solicitud de cancelación para una venta.

## Método de acceso

**GET** /salecancellationrequest

## Estructura de la petición

- **``PartnerSaleIds``**: (``list``) ``Requerido``. Listado de identificadores del colaborador.
- **`FromCreatedDateTime`**: (``date``).  ``Opcional`` Fecha inicial de creación de la transacción. Formato IS0 8601 (YYYY-MM-DD).
- **`ToCreatedDateTime`**: (``date``).  ``Opcional`` Fecha final de creación de la transacción. Formato IS0 8601 (YYYY-MM-DD).
- **`FromUpdatedDateTime`**: (``date``).  ``Opcional`` Fecha inicial de acceso. Formato IS0 8601 (YYYY-MM-DD).
- **`ToUpdatedDateTime`**: (``date``).  ``Opcional`` Fecha final de acceso. Formato IS0 8601 (YYYY-MM-DD).
- **`Page`**: (``int``).  ``Opcional`` Número de página a obtener. Valor por defecto `1`.

### Ejemplo de llamada

??? tip "Ejemplos"

    --8<-- "includes/examples/sale/listOfSaleCancellationRequest.request.1.md"

## Estructura de la respuesta

- **`Timestamp`**: (``dateTime``). Instante de tiempo en el que se procesó la petición. Formato ISO 8601 (yyyy-MM-ddThh\:mm\:ss.fffffff).
- **`Sales`**: (``list``). Listado de ventas.
    - **`PartnerSaleId`**: (``string``). Listado de actividades.
    - **`CancellationRequests`**: (``Objeto``). Conceptos económicos de una venta.
      - **`ExperticketName`**: (``string``). Nombre de Experticket.
        - **`CancellationRequestId`**: (``string``). Identificador de la solicitud de cancelación. 
        - **`SaleId`**: (``Objeto``). Identificador de la venta.
        - **`PartnerSaleId`**: (``string``). Identificador de la venta del colaborador.
        - **`CreatedDateTime`**: (``date``). Fecha de solicitud de cancelación.
        - **`UpdatedDateTime`**: (``date``). Fecha de solicitud de cancelación.
          - **`Status`**: (``string``). Estado de la cancelación.
        
            ??? example "Posibles valores"
                --8<-- "includes/enum/cancellationRequestStatus.md"
        
        - **`StatusComments`**: (``string``). Comentarios del estado de la solicitud de cancelación.
          - **`Reason`**: (``byte``). Estado de la cancelación.
          
            ??? example "Posibles valores"
                --8<-- "includes/enum/cancellationRequestReason.md"
      
        - **`ReasonComments`**: (``string``). Comentarios del estado de la solicitud de cancelación.
- **`PageNumber`**: (``int``). Indica la página solicitada.
- **`HasPreviousPage`**: (``boolean``). Indica si hay una página previa a la solicitada.
- **`HasNextPage`**: (``boolean``). Indica si hay una siguiente página.
- **`IsFirstPage`**: (``boolean``). Indica si la página solicitada corresponde a la primera página

--8<-- "includes/experthubResponseBaseDocumentation.es.md"

### Ejemplo de respuesta

??? tip "Examples"

    --8<-- "includes/examples/sale/listOfSaleCancellationRequest.response.1.md"