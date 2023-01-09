??? tip "Examples"

    === "ProviderIds Filter"

        ``` json
        {
            "ProviderIds": 
            [
                "djifgbvirefnw",
                "39rh3brfn33gb"
            ]
        }
        ```

    === "PrePackageIds Filter"

        ``` json
        {
            "PrePackageIds": 
            [
                "bvqer8bv3b98s",
                "bf34578gbrb29"
            ]
        }
        ```

    === "From/ToDate Filter"

        ``` json
        {
            "FromDate": "2022-06-01",
            "ToDate": "2022-08-01"
        }
        ```

    === "PeopleDistributions Filter"

        ``` json
        {
            "PeopleDistributions": 
            {
                "NumberOfAdults": 2,
                "NumberOfChildren": 2,
                "ChilAges": 
                [
                    10,
                    12
                ]
            }
        }
        ```

    === "Combined Filters"

        ``` json
        {
            "ProviderIds": 
            [
                "djifgbvirefnw",
                "39rh3brfn33gb"
            ],
            "FromDate": "2022-06-01",
            "ToDate": "2022-08-01",
            "PeopleDistributions": 
            {
                "NumberOfAdults": 2,
                "NumberOfChildren": 2,
                "ChilAges": 
                [
                    10,
                    12
                ]
            }
        }
        ```