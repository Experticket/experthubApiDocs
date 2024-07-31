=== "When an activity is added"

    ``` json
    {
        "Success": true,
        "Activities": [
            {
                "Id": "ygqbw4q8owhue",
                "Activity": {
                    "ProductId": "yt1pgb1k61wdc",
                    "Quantity": 1,
                    "AccessDateTime": "2023-01-25T00:00:00",
                    "ForceNotAutoAssignSeating": false
                }
            }
        ]
    }
    ```

=== "When an combined activity is added"

    ``` json
    {
        "Success": true,
        "Activities": [
            {
                "Id": "ygqbw4q8owhue",
                "Activity": {
                    "ProductId": "yt1pgb1k61wdc",
                    "CombinedProductId": "j7gjproc9c6sw",
                    "Quantity": 1,
                    "AccessDateTime": "2023-01-25T00:00:00",
                    "ForceNotAutoAssignSeating": false
                }
            },
             {
                "Id": "sdfhiq8owhue",
                "Activity": {
                    "ProductId": "ppyibu8qwb88s",
                    "CombinedProductId": "j7gjproc9c6sw",
                    "Quantity": 1,
                    "AccessDateTime": "2023-01-26T00:00:00",
                    "ForceNotAutoAssignSeating": false
                }
            }
        ]
    }
    ```

=== "When an accommodation is added"

    ``` json
    {
        "Success": true,
        "Accommodations": [
            {
                "Id": "yhwrziz8bsag1",
                "RateId": "wdiwc9ehmj4yk"
            }
        ]
    }
    ```

=== "When an question is added"

    ``` json
    {
        "Success": true,
        "Activities": [
            {
                "Id": "mi95gbadopeqk",
                "Activity": {
                    "ProductId": "ppyibu8qwb88s",
                    "Quantity": 1,
                    "AccessDateTime": "2023-03-18T00:00:00",
                    "ForceNotAutoAssignSeating": false,
                    "Tickets": [
                        {
                            "TicketId": "5uztgje33ayyw",
                            "Questions": [
                                {
                                    "TicketQuestionId": "6inrbj61drob4",
                                    "StringValue": "response to my question"
                                }
                            ]
                        }
                    ]
                }
            }
        ]
    }
    ```

=== "When a package is added"

    ``` json
    {
        "Success": true,

    }
    ```

=== "When more than one element is added"

    ``` json
    {
        "Success": true,
        "Activities": [
            {
                "Id": "ygqbw4q8owhue",
                "Activity": {
                    "ProductId": "yt1pgb1k61wdc",
                    "Quantity": 1,
                    "AccessDateTime": "2023-01-25T00:00:00",
                    "ForceNotAutoAssignSeating": false
                }
            }
        ],
        "Accommodations": [
            {
                "Id": "yhwrziz8bsag1",
                "RateId": "wdiwc9ehmj4yk"
            }
        ]
    }
    ```