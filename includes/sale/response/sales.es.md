
- **`Sales`**: (``list``). Listado de ventas.
    - **`Activities`**: (``list``). Listado de actividades.
        - [Actividad](../../../docs/es/docs/annex/activity.es.md)
    - **`Accommodations`**: (``list``). Listado de productos combinados de las actividades incluidos en la venta.
          --8<-- "includes/sale/response/accommodation.es.md"
  
    - **`CombinedProducts`**: (``list``). Listado de productos combinados de las actividades incluidos en la venta.
- **`PageNumber`**: (``int``). Indica la página solicitada.
- **`HasPreviousPage`**: (``boolean``). Indica si hay una página previa a la solicitada.
- **`HasNextPage`**: (``boolean``). Indica si hay una siguiente página.
- **`IsFirstPage`**: (``boolean``). Indica si la página solicitada corresponde a la primera página.

--8<-- "includes/experthubResponseBaseDocumentation.es.md"
