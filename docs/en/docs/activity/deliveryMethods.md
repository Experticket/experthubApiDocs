# Delivery methods

As seen when obtaining the [catalog](catalog.md), the tickets have the `RequiresDeliveryManagement` property, which indicates whether a delivery method should be indicated when making the reservation. Using this method it is possible to obtain the available delivery methods and thus complete the necessary information to make the reservation.

## Access method

**GET** activity/deliverymethods

## Request structure

- **`ReservationId`**: (``string``). Identifier of the reservation obtained when confirming the cart.

### Request example

--8<-- "includes/examples/activity/deliveryMethodsQueryExamples.md"

## Response structure

- **`Methods`**: (``list``). Delivery methods array.
    - **`Id`**: (``string``). Delivery method identifier.
    - **`Name`**: (``string``). Delivery method name.
    - **`Description`**: (``string``). Delivery method description.
    - **`Type`**: (``byte``). Delivery method type.

        ??? example "Possible values"
            - 0: Shipping
            - 1: Pickup

    - **`DeliveryPoints`**: (``list``). Delivery points array. This property only appears when `Type == 1` and the delivery method has delivery points set.
        - **`Id`**: (``string``). Delivery point identifier.
        - **`Name`**: (``string``). Delivery point name.
        - **`Address`**: (``string``). Address.
        - **`City`**: (``string``). City.
        - **`ZipCode`**: (``string``). Postal code.
        - **`Province`**: (``string``). Province.
        - **`CountryCode`**: (``string``). *Alpha-2* country code, according to [ISO 3166](https://www.iban.com/country-codes).
        - **`PhoneNumber`**: (``string``). Telephone number.
        - **`Email`**: (``string``). Email.
--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/activity/deliveryMethodsResponseExamples.md"
