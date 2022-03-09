# Método de entrega

Como se ha visto en la [obtención de catálogo](catalog.md), los tickets tienen la propiedad `RequiresDeliveryManagement`, que indica si se debe indicar un método de entrega al realizar la reserva. Usando este método es posible obtener las formas de entrega disponibles y de esta manera completar la información necesaria para realizar la reserva.

## Método de acceso

**GET** activity/deliverymethods

## Estructura de la petición

- **`ReservationId`**: identificador de la reserva obtenido al confirmar el carrito.

### Ejemplo de petición

--8<-- "includes/examples/activity/deliveryMethodsQueryExamples.md"

## Estructura de la respuesta

- **`Methods`**: array de métodos de entrega.
    - **`Id`**: identificador del método de entrega.
    - **`Name`**: nombre del método de entrega.
    - **`Description`**: descripción del método de entrega.
    - **`Type`**: tipo de método de entrega.

        ??? example "Posibles valores"
            - 0: Envío
            - 1: Recogida

    - **`DeliveryPoints`**: array de puntos de entrega. Esta propiedad sólo aparece cuando `Type == 1` y el método de entrega tiene puntos de entrega establecidos.
        - **`Id`**: identificador del punto de entrega.
        - **`Name`**: nombre del punto de entrega.
        - **`Address`**: dirección.
        - **`City`**: ciudad.
        - **`ZipCode`**: código postal.
        - **`Province`**: provincia.
        - **`CountryCode`**: código *Alpha-2* del país, según la [norma ISO 3166](https://www.iban.com/country-codes).
        - **`PhoneNumber`**: número de teléfono.
        - **`Email`**: correo electrónico.
--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/deliveryMethodsResponseExamples.md"
