# Comprobar método de entrega

Mediante esta llamada se comprueba si un método de entrega permite el envío a una dirección, el plazo estimado de entrega y el coste asociado.

## Método de acceso

**GET** activity/deliverymethodcheck

## Estructura de la petición

- **`ReservationId`**: (``string``). Identificador de la reserva obtenido al confirmar el carrito.
- **`DeliveryMethodId`**: (``string``). Identificador del método de entrega obtenido en la llamada a [métodos de entrega](deliveryMethods.md).
- **`CountryCode`**: (``string``). Código *Alpha-2* del país, según la [norma ISO 3166](https://www.iban.com/country-codes).
- **`ZipCode`**: (``string``). Código postal.

### Ejemplo de petición

--8<-- "includes/examples/activity/checkDeliveryMethodsQueryExamples.md"

## Estructura de la respuesta

- **`ShippingCosts`**: (``decimal``). Gastos de envío.
- **`DeliveryDays`**: (``short``). Estimación de los días necesarios para que los productos lleguen a su destino.
--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/checkDeliveryMethodsResponseExamples.md"
