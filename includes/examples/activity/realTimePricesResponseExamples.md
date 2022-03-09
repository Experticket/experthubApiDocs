=== "ProductIds & AccessDates"

    ``` json
    {
        "ProductsRealTimePrices": [
            {
                "ProductId": "dj48vjsyufvyu",
                "AccessDate": "2020-01-02",
                "Price": 29,
                "PriceMode": 1,
                "Success": true
            },
            {
                "ProductId": "dj48vjsyufvyu",
                "AccessDate": "2022-05-15",
                "Price": 35,
                "PriceMode": 1,
                "Success": true
            },
            {
                "ProductId": "ajr7v0alt62hl",
                "AccessDate": "2020-01-02",
                "Price": 18,
                "PriceMode": 1,
                "Success": true
            },
            {
                "ProductId": "ajr7v0alt62hl",
                "AccessDate": "2022-05-15",
                "Price": 22,
                "PriceMode": 1,
                "Success": true
            }
        ],
        "Success": true,
        "Timestamp": "2022-02-18T17:02:27.8165916"
    }
    ```

=== "ProductIds & Start/EndDate"

    ``` json
    {
        "ProductsRealTimePrices": 
        [
            {
                "ProductId": "dj48vjsyufvyu",
                "AccessDate": "2020-01-02",
                "Price": 29,
                "PriceMode": 1,
                "Success": true,
                "Timestamp": "2022-02-18T17:02:27.8165916"
            },
            {
                "ProductId": "dj48vjsyufvyu",
                "AccessDate": "2022-05-03",
                "Price": 35,
                "PriceMode": 1,
                "Success": true,
                "Timestamp": "2022-02-18T17:02:27.8165916"
            },
            {
                "ProductId": "dj48vjsyufvyu",
                "AccessDate": "2020-01-04",
                "Price": 20,
                "PriceMode": 1,
                "Success": true,
                "Timestamp": "2022-02-18T17:02:27.8165916"
            }
        ],
        "Success": true,
        "Timestamp": "2022-02-18T17:02:27.8165916"
    }
    ```

=== "CombinedProducts"

    ``` json
    {
        "ProductsRealTimePrices": 
        [
            {
                "CombinedProductId": "iudhbfvifebvi",
                "CombinedProductProducts": 
                [
                    {
                        "ProductId": "jiufdv80querb",
                        "AccessDate": "2022-05-03"
                    },
                    {
                        "ProductId": "349u8g870r3vb",
                        "AccessDate": "2022-05-05"
                    }
                ],
                
                "Price": 59.54,
                "PriceMode": 1,
                "Success": true,
                "Timestamp": "2022-02-18T17:02:27.8165916"
            }
        ],
        "Success": true,
        "Timestamp": "2022-02-18T17:02:27.8165916"
    }
    ```
