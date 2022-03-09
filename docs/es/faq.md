# Preguntas frecuentes

## Actividades

??? faq "¿Tengo que consultar el catálogo con cada venta que realice?"
    No, el catálogo debe procesarse una vez y únicamente repetir este proceso en caso de que cambie su fecha de actualización. Esto lo podemos ver comparando la fecha del catálogo con la fecha que nos devuelva el endpoint [última fecha de actualización del catálogo](docs/activity/lastCatalogUpdatedDate.md).

??? faq "¿Cuándo tengo que consultar la disponibilidad de un producto o una sesión?"
    Unicamente debemos consultar la disponibilidad de aquellos productos que tengan definidos en el [catálogo](docs/activity/catalog.md) el campo ``DaysWithLimitedCapacity`` o aquellas [sesiones](docs/activity/sessions.md) que tengan definido el campo AvailableCapacity.

## Carrito y venta

??? faq "¿Puedo añadir productos al carrito con cantidad 0?"
    No, el sistema no admite añadir productos con cantidad menor de 1. Podría provocar un error que permitiese confirmar el carrito pero no confirmar la venta.

??? faq "¿Es obligatorio indicar todos los datos del cliente al confirmar la venta?"
    No. A nivel técnico, como se especifica en la [documentación](), únicamente son obligatorios el nombre y los apellidos. Es posible que en el proceso de certificación del API algunos clientes exijan otros datos como el correo, el DNI, etc.

    Hay que tener en cuenta que aquellos campos que no se deseen enviar no deben ser enviados o enviados como null, no es posible indicar los campos con un string vacío, ya que en ese caso el sistema interpreta que están definidos y comprueba que el formato de dichos datos sea correcto.
