=== "Add an activity"

    ``` json
    {
        "ShoppingCartId": "stf9gy7i3xawa",
        "Activities": [
            {
                "ProductId": "yt1pgb1k61wdc",
                "AccessDateTime": "2023-01-25",
                "Quantity": 1
            }
        ]
    }
    ```

=== "Add a combined activities(Combined product)"

    ``` json
    {
        "ShoppingCartId": "stf9gy7i3xawa",
        "Activities": [
            {
                "ProductId": "yt1pgb1k61wdc",
                "CombinedProductId": "j7gjproc9c6sw",
                "AccessDateTime": "2023-01-25",
                "Quantity": 1
            },
            {
                "ProductId": "ppyibu8qwb88s",
                "CombinedProductId": "j7gjproc9c6sw",
                "AccessDateTime": "2023-01-26",
                "Quantity": 1
            }
        ]
    }
    ```

=== "Add an accommodation"

    ``` json
    {
        "ShoppingCartId": "stf9gy7i3xawa",
        "Accommodations": [
            {
                "EchoToken": "aa5zyx8djys5az9msuhjzcoqge",
                "Rates": [
                    "wdiwc9ehmj4yk"
                ]
            }
        ]
    }
    ```

=== "Add a question"

    ``` json
    {
        "ShoppingCartId": "48siun8ozecx1",
        "Activities": [
            {
                "ProductId": "ppyibu8qwb88s",
                "AccessDateTime": "2023-03-18",
                "Quantity": 1,
                "Tickets": [
                    {
                        "TicketId": "5uztgje33ayyw",
                        "Questions": [
                            {
                                "TicketQuestionId": "6inrbj61drob4",
                                "StringValue": "response of my question"
                            }
                        ]
                    }
                ]
            }
        ]
    }
    ```

=== "Add a package"

    ``` json
    {
        "ShoppingCartId": "stf9gy7i3xawa",
        "Packages": [
            {
                "EchoToken": "az9msuhjzcoqgeaa5zyx8djys5",
                "Packages": [
                    {
                        "Id": "4pdc7ad88qota"
                    }
                ]
            }
        ]
    }
    ```

=== "Add a package with sessions and question"

    ``` json
    {
        "ShoppingCartId": "hy3gp7cykreog",
        "Activities": [
            {
                "ProductId": "35ro8mcqkzs4q",
                "AccessDateTime": "2023-03-21",
                "Quantity": 1,
                "Tickets": [
                    {
                        "TicketId": "6nx1a1pd1wbms",
                        "Questions": [
                            {
                                "TicketQuestionId": "dhci15yyp1y81",
                                "StringValue": "respuesta"
                            }
                        ],
                        "SessionId": "9zobybtjtou6s",
                        "AccessDateTime": "2023-03-21"
                    }
                ]
            }
        ]
    }
    ```

=== "Add more than one element"

    ``` json
    {
        "ShoppingCartId": "{{ShoppingCartId}}",
        "Activities": [
            {
                "ProductId": "yt1pgb1k61wdc",
                "AccessDateTime": "2023-01-25",
                "Quantity": 1
            }
        ],
        "Accommodations": [
            {
                "EchoToken": "{{EchoToken}}",
                "Rates": [
                    "wdiwc9ehmj4yk"
                ]
            }
        ]
    }
    ```