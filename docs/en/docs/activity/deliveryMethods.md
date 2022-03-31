# Delivery methods

As seen when obtaining the [catalog](catalog.md), the tickets have the `RequiresDeliveryManagement` property, which indicates whether a delivery method should be indicated when making the reservation. Using this method it is possible to obtain the available delivery methods and thus complete the necessary information to make the reservation.

## Access method

**GET** activity/deliverymethods

## Request structure

- **`ReservationId`**: identifier of the reservation obtained when confirming the cart.

### Request example

--8<-- "includes/examples/activity/deliveryMethodsQueryExamples.md"

## Response structure

- **`Methods`**: delivery methods array.
    - **`Id`**: delivery method identifier.
    - **`Name`**: delivery method name.
    - **`Description`**: delivery method description.
    - **`Type`**:  delivery method type.

        ??? example "Possible values"
            - 0: Shipping
            - 1: Pickup

    - **`DeliveryPoints`**: delivery point array. This property will only apper if `Type == 1` and the delivery method has delivery points defined.
        - **`Id`**: delivery point identifier.
        - **`Name`**: delivery point name.
        - **`Address`**: address.
        - **`City`**: city.
        - **`ZipCode`**: postal code.
        - **`Province`**: province.
        - **`CountryCode`**: *Alpha-2* country code, according to [ISO 3166](https://www.iban.com/country-codes).
        - **`PhoneNumber`**: telephone number.
        - **`Email`**: email.
--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/activity/deliveryMethodsResponseExamples.md"
