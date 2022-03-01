``` json
{
    "Rules": 
    [        
        {
            "Id" : "zz4fnju76ysb1",
            "Name": "Regla descuento",
            "Order": 1,
            "Inputs": 
            [
                {
                    "ProductId": "twy5yhbishk91"
                },
                {
                    "ProductId": "uspeg7nr5st96"
                }
            ],
            "Processors": 
            [
                {
                    "Value": 1,
                    "OutputIfExistsApplicability": 0,
                    "Outputs": 
                    [
                        {
                            "ProductId": "twy5yhbishk91",
                            "Order": 1,
                            "Quantity": 1,
                            "ApplicationType": 2,
                            "PriceModifierType": 3,
                            "PriceModifierValue": 5.000000000000
                        }
                    ]
                }
            ]
        },
        {
            "Id" : "hy8fnju42ycf4",
            "Name": "Regla producto gratis 3x2",
            "Order": 2,
            "Inputs": 
            [
                {
                    "ProductId": "hwuk9huaqopwo"
                }
            ],
            "Processors": 
            [
                {
                    "Value": 2,
                    "OutputIfExistsApplicability": 0,
                    "Outputs": 
                    [
                        {
                            "ProductId": "twy5yhbishk91",
                            "Order": 1,
                            "Quantity": 1,
                            "ApplicationType": 1,
                            "PriceModifierType": 1,
                            "PriceModifierValue": 100.000000000000
                        }
                    ]
                }
            ]
        }
    ],
    "Success": true,
    "Timestamp": "2021-02-18T17:02:27.8165916"
}
```
