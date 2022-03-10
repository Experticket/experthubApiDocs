=== "Simple"

    ``` json
    {
        "Products": 
        [
            {
                "ProductId": "hwuk9huaqopwo",
                "Quantity": 4,
                "AccessDate": "2022-06-02"
            }
        ]
    }
    ```

=== "With Ticket"

    ``` json
    {
        "Products": [
            {
                "ProductId": "hwuk9huaqopwo",
                "Quantity": 4,
                "AccessDate": "2022-06-02",
                "Tickets": 
                [
                    {
                        "TicketId": "654e5ytetr"
                    }
                ]
            }
        ]
    }
    ```

=== "With Ticket & AccessDate"

    ``` json
    {
        "Products": [
            {
                "ProductId": "hwuk9huaqopwo",
                "Quantity": 4,
                "AccessDate": "2022-06-02",
                "Tickets": 
                [
                    {
                        "TicketId": "654e5ytetr",
                        "AccessDate": "2022-06-05"
                    }
                ]
            }
        ]
    }
    ```
