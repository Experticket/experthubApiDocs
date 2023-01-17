# Método de entrega

Como se ha visto en la [obtención de catálogo](catalog.md), los tickets tienen la propiedad `RequiresDeliveryManagement`, que indica si se debe indicar un método de entrega al realizar la reserva. Usando este método es posible obtener las formas de entrega disponibles y de esta manera completar la información necesaria para realizar la reserva.

## Método de acceso

**GET** activity/deliverymethods

## Estructura de la petición

- **`ReservationId`**: (``string``). Identificador de la reserva obtenido al confirmar el carrito.

### Ejemplo de petición

--8<-- "includes/examples/activity/deliveryMethodsQueryExamples.md"

## Estructura de la respuesta

- **`Methods`**: (``list``). Array de métodos de entrega.
    - **`Id`**: (``string``). Identificador del método de entrega.
    - **`Name`**: (``string``). Nombre del método de entrega.
    - **`Description`**: (``string``). Descripción del método de entrega.
    - **`Type`**: (``byte``). Tipo de método de entrega.

        ??? example "Posibles valores"
            - 0: Envío
            - 1: Recogida

    - **`DeliveryPoints`**: (``list``). Array de puntos de entrega. Esta propiedad sólo aparece cuando `Type == 1` y el método de entrega tiene puntos de entrega establecidos.
        - **`Id`**: (``string``). Identificador del punto de entrega.
        - **`Name`**: (``string``). Nombre del punto de entrega.
        - **`Address`**: (``string``). Dirección.
        - **`City`**: (``string``). Ciudad.
        - **`ZipCode`**: (``string``). Código postal.
        - **`Province`**: (``string``). Provincia.
        - **`CountryCode`**: (``string``). Código *Alpha-2* del país, según la [norma ISO 3166](https://www.iban.com/country-codes).
        - **`PhoneNumber`**: (``string``). Número de teléfono.
        - **`Email`**: (``string``). Correo electrónico.
--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/deliveryMethodsResponseExamples.md"
