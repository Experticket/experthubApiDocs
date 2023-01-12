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