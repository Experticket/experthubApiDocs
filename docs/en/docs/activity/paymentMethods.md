# Payment methods

This is an intermediate step that we must perform before confirming the cart. See the ``PartnerSettings`` field in the [catalog](catalog.md).

!!! success ""
    If **``PaymentType``** in the catalog indicates that our payment method is different from debit, this call is irrelevant for us.
!!! warning ""
    If **``PaymentType``** in the catalog indicates that our payment method to the distributor is debit, we must use this call.

## Access method

**GET** activity/paymentmethods

## Request data structure

- **`ReservationId`**: reservation identifier obtained when confirming the cart.

### Request example

--8<-- "includes/examples/activity/paymentMethodsQueryExamples.md"

## Response data structure

- **`PaymentMethods`**: array of payment methods.
    - **``Type``**: payment method type identifier.
    - **``Name``**: payment method name.
    - **``EnableSendByEmails``**: indicates if we can use this payment method to automatically send a payment link to the end customer via email.
- **`Success`**: boolean `#!csharp true/false` that indicates whether or not the call was processed correctly.
- **`Timestamp`**: instant of time in which the request was processed. *ISO 8601 format (yyyy-MM-ddThh:mm:ss.fffffff)*.
- **`ErrorMessage`**: error message explaining why the request was not successful. If it was correct, it will return `#!csharp null`.

### Response example

--8<-- "includes/examples/activity/paymentMethodsResponseExamples.md"
