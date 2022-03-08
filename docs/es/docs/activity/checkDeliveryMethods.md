# Comprobar método de entrega

Mediante esta llamada se comprueba si un método de entrega permite el envío a una dirección, el plazo estimado de entrega y el coste asociado.

## Método de acceso

**GET** activity/deliverymethodcheck

## Estructura de la petición

- **`PartnerId`**: identificador del colaborador.
- **`ReservationId`**: identificador de la reserva obtenido al confirmar el carrito.
- **`DeliveryMethodId`**: identificador del método de entrega obtenido en la llamada a [métodos de entrega](deliveryMethods.md).
- **`CountryCode`**: código *Alpha-2* del país, según la [norma ISO 3166](https://www.iban.com/country-codes).
- **`ZipCode`**: código postal.

### Ejemplo de petición

--8<-- "includes/examples/activity/paymentMethodsQueryExamples.md"

## Estructura de la respuesta

- **`ShippingCosts`**: gastos de envío.
- **`DeliveryDays`**: estimación de los días necesarios para que los productos lleguen a su destino.
--8<-- "includes/responseBaseDocumentation.es.md"
