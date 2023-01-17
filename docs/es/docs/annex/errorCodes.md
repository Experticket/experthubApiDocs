# Códigos de error

En este anexo se definen los códigos de error que pueden devolver la API en cada llamada y su significado.

!!! important "IMPORTANTE"
    No todos los errores devolverán un ErrorCode, iremos añadiendo poco a poco todos los casos.

Lista de códigos de errores:

- **5000**: El documento de identificación del cliente es requerido (DNI, NIF, Pasaporte...).
- **5001**: Se ha excedido el importe diario máximo de ventas para el cliente indicado. Para poder realizar la venta debe indicarse el nombre del cliente y la dirección completa.
- **5002**: Se ha excedido el importe diario máximo de ventas para el cliente indicado, por favor póngase en contacto con el departamento indicado en el mensaje de error.
