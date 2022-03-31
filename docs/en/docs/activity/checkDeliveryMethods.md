# Check delivery method

This call checks if a delivery method allows delivery to an address, the estimated delivery time and the associated cost.

## Access method

**GET** activity/deliverymethodcheck

## Request structure

- **`ReservationId`**: reservation identifier obtained when confirming the cart.
- **`DeliveryMethodId`**: identifier of the delivery method obtained in the call to [delivery methods](deliveryMethods.md).
- **`CountryCode`**: country *Alpha-2* code, according to [ISO 3166 standard](https://www.iban.com/country-codes).
- **`ZipCode`**: postal code.

### Request example

--8<-- "includes/examples/activity/checkDeliveryMethodsQueryExamples.md"

## Response structure

- **`ShippingCosts`**: shipping costs.
- **`DeliveryDays`**: estimation of the days needed for the products to arrive at their destination.
--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/activity/checkDeliveryMethodsResponseExamples.md"
