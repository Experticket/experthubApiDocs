``` json
{
    "Products": [
        {
            "ProductId": "MyProductId01",
            "AccessDate": "2026-07-15T00:00:00",
            "ProviderId": "prov12345abcd",
            "Tickets": [
                {
                    "TicketId": "MyTicketId01",
                    "SessionId": null,
                    "TicketQuestionsProfileId": "pdk563qjqkyns",
                    "AccessDate": "2026-07-15T00:00:00"
                }
            ]
        }
    ],
    "Providers": [
        {
            "ProviderId": "prov12345abcd",
            "ProviderQuestionsProfileIds": [ "prv8q2k9wla3c" ]
        }
    ],
    "TicketQuestionsProfiles": [
        {
            "Id": "pdk563qjqkyns",
            "Name": "Datos del asistente",
            "CommercialName": null,
            "AreDynamicQuestions": false,
            "Questions": [
                {
                    "Id": "xsdt8tj1g9zrh",
                    "Question": "Nombre del asistente",
                    "ShortQuestion": "Nombre",
                    "Required": true,
                    "DataType": 0
                }
            ]
        }
    ],
    "ProviderQuestionsProfiles": [
        {
            "Id": "prv8q2k9wla3c",
            "Name": "Matrícula del vehículo",
            "AreDynamicQuestions": false,
            "Questions": [
                {
                    "Id": "q1mat5kz9p2rt",
                    "Question": "Matrícula del vehículo",
                    "ShortQuestion": "Matrícula",
                    "Required": true,
                    "DataType": 0,
                    "RegexValidationPattern": "^[0-9]{4}[A-Z]{3}$",
                    "RegexValidationErrorMessage": "Formato de matrícula no válido"
                }
            ]
        }
    ],
    "SaleQuestionsProfiles": [
        {
            "Id": "sale7yq2k9wla",
            "Name": "Origen de la reserva",
            "AreDynamicQuestions": false,
            "Questions": [
                {
                    "Id": "qorigen3k9wla",
                    "Question": "¿Cómo nos conociste?",
                    "ShortQuestion": "Origen",
                    "Required": false,
                    "DataType": 10,
                    "Values": [
                        { "Text": "Internet", "Value": "web" },
                        { "Text": "Recomendación", "Value": "ref" }
                    ]
                }
            ]
        }
    ],
    "ClientQuestionsProfiles": [
        {
            "Id": "cli9q2k9wla3c",
            "Name": "Preferencias del cliente",
            "AreDynamicQuestions": false,
            "Questions": [
                {
                    "Id": "qnews3k9wla3c",
                    "Question": "¿Deseas recibir novedades por email?",
                    "ShortQuestion": "Novedades",
                    "Required": false,
                    "DataType": 2
                }
            ]
        }
    ],
    "Success": true,
    "Timestamp": "2026-06-11T00:00:00"
}
```
