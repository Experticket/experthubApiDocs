# Payment methods

This is an intermediate step that must be performed before confirming the cart. See the `PartnerSettings` field in the [catalog](catalog.md).

!!! success ""
    If **`PaymentType`** in the catalog indicates that our payment method is different from debit, this call is irrelevant for us.
!!! warning ""
    If **`PaymentType`** in the catalog indicates that our payment method to the distributor is debit, this call must be used.

## Access method

**GET** activity/paymentmethods

## Request structure

- **`ReservationId`**: (`string`). Reservation identifier obtained when confirming the cart.

### Request example

--8<-- "includes/examples/activity/paymentMethodsQueryExamples.md"

## Response structure

- **`PaymentMethods`**: (`list`). Array of payment methods.
  - **`Id`**: (`string`). Payment method identifier.
  - **`Type`**: (`byte`). Payment method type.
  - **`Name`**: (`string`). Payment method name.
  - **`CommercialName`**: (`string`) `Optional`. Payment method commercial name.
  - **`EnableSendByEmail`**: (`boolean`) `Optional`. Indicates whether this payment method can be used to automatically send a payment link by email.
  - **`Fields`**: (`list`). Array of fillable fields associated with the payment method. These fields can be specified when creating a transaction.
    - **`Id`**: (`string`). Field identifier.
    - **`Name`**: (`string`). Field name.
    - **`IsRequired`**: (`boolean`). Indicates whether the field is required.
    - **`RegexValidation`**: (`string`) `Optional`. Regular expression that the value entered in the field must satisfy.
    - **`RegexValidationErrorMessage`**: (`string`) `Optional`. Error message to show to the user if the regular expression is not satisfied.
    - **`DefaultValue`**: (`string`) `Optional`. Default field value to show to the user.
    - **`DataType`**: (`byte`). Indicates the data type the field value must have.

        ??? example "Possible values"
            - 0: Text
            - 1: Numeric
            - 2: Date
            - 3: Boolean

--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/activity/paymentMethodsResponseExamples.md"
