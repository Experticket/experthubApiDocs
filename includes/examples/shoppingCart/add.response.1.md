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