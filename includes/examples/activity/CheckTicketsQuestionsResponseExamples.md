=== "Pregunta Texto"

    ``` json
    {
        {
        "TicketQuestionsProfiles": [
            {
                "Id": "pdk563qjqkyns",
                "AreDynamicQuestions": false,
                "Questions": [
                    {
                        "Id": "xsdt8tj1g9zrh",
                        "Required": false,
                        "DataType": 0,
                        "RegexValidationPattern": "patron validación",
                        "RegexValidationErrorMessage": "mensaje error"
                    }
                ]
            }
        ],
        "Success": true,
        "Timestamp": "2023-03-13T00:00:00"
        }
    }
    ```
=== "Pregunta Booleano"

    ``` json
    {
        {
            "TicketQuestionsProfiles": [
                {
                    "Id": "pdk563qjqkyns",
                    "AreDynamicQuestions": false,
                    "Questions": [
                        {
                            "Id": "89tbrdp6gi6oh",
                            "Question": "pregunta booleano",
                            "ShortQuestion": "corta booleao",
                            "Required": false,
                            "DataType": 2
                        }
                    ]
                }
            ],
            "Success": true,
            "Timestamp": "2023-03-13T00:00:00"
        }
    }
    ```

=== "Pregunta Fecha"

    ``` json
        {
            "TicketQuestionsProfiles": [
                {
                    "Id": "pdk563qjqkyns",
                    "AreDynamicQuestions": false,
                    "Questions": [
                        {
                            "Id": "zfufit3d3kofa",
                            "Question": "Pregunta Fecha",
                            "ShortQuestion": "pregunta abreviada ",
                            "Required": false,
                            "DataType": 4
                        }
                    ]
                }
            ],
            "Success": true,
            "Timestamp": "2023-03-13T00:00:00"
        }
    ```
=== "Pregunta Número Entero"

    ``` json
        {
            "TicketQuestionsProfiles": [
                {
                    "Id": "pdk563qjqkyns",
                    "AreDynamicQuestions": false,
                    "Questions": [
                        {
                            "Id": "dz5877yi6wjfk",
                            "Question": "preguntna numero entero",
                            "ShortQuestion": "abreviada entero",
                            "Required": false,
                            "DataType": 6
                        }
                    ]
                }
            ],
            "Success": true,
            "Timestamp": "2023-03-13T00:00:00"
        }
    ```
=== "Pregunta Número Entero"

    ``` json
        {
            "TicketQuestionsProfiles": [
                {
                    "Id": "pdk563qjqkyns",
                    "AreDynamicQuestions": false,
                    "Questions": [
                        {
                            "Id": "86h1dnjfzy6ma",
                            "Question": "¿Pregunta principal para decimal?",
                            "ShortQuestion": "pregunta corta",
                            "Required": false,
                            "DataType": 8
                        }
                    ]
                }
            ],
            "Success": true,
            "Timestamp": "2023-03-13T00:00:00"
        }
    ```
=== "Pregunta selección de un valor entre un conjunto de valores predefinidos"

    ``` json
        {
            "TicketQuestionsProfiles": [
                {
                    "Id": "pdk563qjqkyns",
                    "AreDynamicQuestions": false,
                    "Questions": [
                        {
                            "Id": "4gc7t9kb6aark",
                            "Question": "¿Pregunta principal para seleccionar uno?",
                            "ShortQuestion": "pregunta corta",
                            "Required": false,
                            "DataType": 10,
                            "Values": []
                        }
                    ]
                }
            ],
            "Success": true,
            "Timestamp": "2023-03-13T00:00:00"
        }
    ```
=== "Pregunta selección de varios valores entre un conjunto de valores predefinidos"

    ``` json
        {
            "TicketQuestionsProfiles": [
                {
                    "Id": "pdk563qjqkyns",
                    "AreDynamicQuestions": false,
                    "Questions": [
                        {
                            "Id": "p68wgknpsgx4c",
                            "Question": "¿Pregunta principal para seleccionar varios?",
                            "ShortQuestion": "¿Pregunta corta?",
                            "Required": false,
                            "DataType": 11,
                            "MaxNumberOfValues": 2,
                            "Values": []
                        }
                    ]
                }
            ],
            "Success": true,
            "Timestamp": "2023-03-13T00:00:00"
        }
    ```
=== "Pregunta Archivos"

    ``` json
        {
            "TicketQuestionsProfiles": [
                {
                    "Id": "pdk563qjqkyns",
                    "AreDynamicQuestions": false,
                    "Questions": [
                        {
                            "Id": "8bkbihetazhcs",
                            "Question": "¿Pregunta principal para archivos?",
                            "ShortQuestion": "¿Pregunta corta?",
                            "Required": false,
                            "DataType": 12
                        }
                    ]
                }
            ],
            "Success": true,
            "Timestamp": "2023-03-13T00:00:00"
        }
    ```