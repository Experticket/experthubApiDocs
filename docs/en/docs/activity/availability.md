# Available capacity

As we have seen in the point [obtain catalog](catalog.md), both ``ProductBases`` and ``Products`` have the property **``DaysWithLimitedCapacity``**, as well as through the [call to get sessions](sessions.md) we see that ``Sessions`` can have **``AvailableCapacity``** defined.

!!! success ""
    If the field ``DaysWithLimitedCapacity`` is empty and, in case the product has non-auto assigned sessions (see in [catalog](catalog.md)), if the sessions do not have the ``AvailableCapacity`` field defined means that you do not have to check the availability for any date, therefore it is not necessary to make this API call.

!!! warning ""
    If the ``DaysWithLimitedCapacity`` field has days defined or the sessions have ``AvailableCapacity`` defined, we must check the available capacity of the category (ProductBase), the product, and/or the corresponding session before offering the product to the customer.

!!! error ""
    If when trying to confirm the cart the capacity has been exceeded, that is, there is not enough capacity left to carry out the reservation, an error will be returned.

Available capacity refers to quota type tickets (``#!csharp IsQuotaTicket == true``). Therefore, the capacity of a product is the number of quota type tickets that can be sold for that product. And the capacity of a ProductBase is the amount of quota type tickets that can be sold from the sum of all products of the ProductBase.

??? info "Example"
    Obtain the following information from the catalog:

    - The following ``ProductBase`` has November 1, 2022 marked as the date on which availability must be checked.

        ``` json hl_lines="3"
        {
            "ProductBaseId": "gfo753rgjfbw6",
            "DaysWithLimitedCapacity": "2022-11-01"
        }
        ```
    - The following ``Product`` has August 15 and April 17, 2022 marked as dates to check availability.

        ``` json hl_lines="3"
        {
            "ProductId": "htgy4tgm9q21n",
            "DaysWithLimitedCapacity": "2022-04-17,2022-08-15"
        }
        ```
    - The following ``Product`` has two sessions, both with ``AvailableCapacity`` defined, so its availability must be checked.

        ``` json hl_lines="7"
        {
            "ProductId": "q2oghu9mye7h2",
            "Tickets": [
                {
                    "TicketId": "fb8mcqxyo22rg",
                    "IsQuotaTicket": true,
                    "TicketEnclosureId": "g5u6m3xew6hxy"
                }
            ]
        }
        ```
        ``` json hl_lines="5 6 7"
        {
            "TicketEnclosureId": "g5u6m3xew6hxy",
            "Sessions": 
            {
                "SessionContentProfileId ": "dkjvidkfjkdfv",
                "SessionGroupProfileId": "dfjbfqwe8934d",
                "TicketEnclosureAutoAssignSessionType": 0
            }
        }
        ```

        When [getting the sessions](sessions.md) we see the following:

        ``` json hl_lines="6 11"
        {
        "Sessions": [
            {
                "SessionId": "5b8qkqnmhdmk1",
                "SessionTime": "2021-06-21T10:00:00",
                "AvailableCapacity": 165
            },
            {
                "SessionId": "5o3bwhx1ze1m1",
                "SessionTime": "2021-09-06T10:00:00",
                "AvailableCapacity": 230
            },
            {
                "SessionId": "sdviufdnvr843",
                "SessionTime": "2021-09-06T17:00:00"
            }
        ]
        }
        ```

    - The following ``Product`` is made up of three capacity-type tickets. So, if the capacity of the product were 9, we could only sell 3 products. And if the capacity was 16, we could only sell 5 products.

        ``` json hl_lines="6 10 14"
        {
            "ProductId": "htgy4tgm9q21n",
            "Tickets": [
                {
                    "TicketId": "1tqgtrf7ctefc",
                    "IsQuotaTicket": true
                }, 
                {
                    "TicketId": "2lob55g8w3fff",
                    "IsQuotaTicket": true
                }, 
                {
                    "TicketId": "jkp78j40cnfh3",
                    "IsQuotaTicket": true
                }, 
                {
                    "TicketId": "gggsijt911am4",
                    "IsQuotaTicket": false
                }
            ]
        }
        ```
    - The following ``ProductBase`` is made up of a product with a capacity-type ticket and another product with three capacity-type tickets:

        ``` json hl_lines="10 14 18 31"
        {
            "ProductBaseId": "gfo753rgjfbw6",
            "DaysWithLimitedCapacity": "2022-08-31",
            "Products": [
                {
                    "ProductId": "htgy4tgm9q21n",
                    "Tickets": [
                        {
                            "TicketId": "1tqgtrf7ctefc",
                            "IsQuotaTicket": true
                        }, 
                        {
                            "TicketId": "2lob55g8w3fff",
                            "IsQuotaTicket": true
                        }, 
                        {
                            "TicketId": "jkp78j40cnfh3",
                            "IsQuotaTicket": true
                        }, 
                        {
                            "TicketId": "gggsijt911am4",
                            "IsQuotaTicket": false
                        }
                    ]
                },
                {
                    "ProductId": "q2oghu9mye7h2",
                    "Tickets": [
                        {
                            "TicketId": "fb8mcqxyo22rg",
                            "IsQuotaTicket": true
                        }
                    ]
                }
            ]
        }
        ```

        So, if the capacity of the ``ProductBase`` were 21, we could sell combinations like the following:

          - 21 products of "q2oghu9mye7h2" (21 x 1 = 21)
          - 7 products of "htgy4tgm9q21n" (7 x 3 = 21)
          - 6 products of "q2oghu9mye7h2" and 5 of "htgy4tgm9q21n" (6 x 1 + 5 x 3 = 21)
          - 15 products of "q2oghu9mye7h2" and 3 of "htgy4tgm9q21n" (15 x 1 + 3 x 3 = 21)
          - And any other combination we can think of.

## Access Method

**POST** /availablecapacity

## Request data structure

- **`ProductBaseIds`**: array of category identifiers to filter by.
- **`ProductIds`**: array of product identifiers to filter by.
- **`SessionIds`**: array of session identifiers to filter by.
- **`Dates`**: array of dates to filter by. *ISO 8601 format (yyyy-MM-dd)*.
- **`FromDate`**: if you want to filter by a range of dates, you can filter by start date. Does not allow values prior to today. Its default value is today. *ISO 8601 format (yyyy-MM-dd)*.
- **`ToDate`**: if you want to filter by a range of dates, you can filter by end date. Its default value is the date corresponding to one year from now. *ISO 8601 format (yyyy-MM-dd)*.

!!! tip "Important"
    At least one `ProductBaseId`, `ProductId`, or `SessionId` must be defined. You can add as many as you want and they will be considered an ***OR***.

### Request example

--8<-- "includes/examples/activity/availabilityQueryExamples.md"

## Response data structure

- **`ProductBases`**: array containing the requested `ProductBase`. Corresponds to each day with limited access to each of the `ProductBase`.
    - **`ProductBaseId`**: identifier of the `ProductBase`.
    - **`Date`**: access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **`AvailableCapacity`**: capacity available for sale.
- **`Products`**: array containing the requested products. Corresponds to each day with limited access to each of the products.
    - **`ProductId`**: identificador del producto.
    - **`Date`**: access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **`AvailableCapacity`**: capacity available for sale.
- **`Sessions`**: array containing the requested sessions. Corresponds to each day with limited access to each of the sessions.
    - **`SessionId`**: identificador de la sesión.
    - **`Date`**: access date. *ISO 8601 format (yyyy-MM-ddThh:mm:ss.fffffff)*.
    - **`AvailableCapacity`**: capacity available for sale.
--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/activity/availabilityResponseExamples.md"
