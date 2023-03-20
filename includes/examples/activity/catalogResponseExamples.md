``` json
{
    "Success": true,
    "Timestamp": "2022-01-01T17:02:27.8165916",
    "ErrorMessage": null,
    "Providers": 
    [
        {
            "ProviderId": "by81fymhsmjgw",
            "ProviderName": "PTM",
            "ProviderDescription": "Provider Description",
            "ProviderAccessConditions": "Provider access conditions",
            "ExchangeVoucherPoint": "Access point",
            "AccessCodeMethodName": "TicketWaitForIt",
            "AdvancedDateSelectorMethodName": "None",
            "CancellationPolicy": 
            {
                "IsRefundable": true,
                "Rules": 
                [
                    {
                        "HoursInAdvanceOfAccess": 6,
                        "Percentage": 80
                    },
                    {
                        "HoursInAdvanceOfAccess": 120,
                        "Percentage": 75
                    }
                ]
            },
            "IsForGroups": false,
            "LimitOfNumberOfPeopleToBeGroup": 19,
            "Logo": "https://url.ofthelogo.com",
            "Location": 
            {
                "CountryCode": "es",
                "City": "Torrevieja",
                "Address": "Avda. Delfina Viudes, 99",
                "ZipCode": "03183",
                "Lat": 37.99,
                "Lng": -0.68,
                "Region": "Alicante"
            },
            "Urls": 
            [
                {
                    "LanguageCode": "es",
                    "Url": "https://url.com/park1"
                },
                {
                    "LanguageCode": "en",
                    "Url": "https://en-url.com/park1"
                }
            ],
            "TicketEnclosures": 
            [
                {
                    "TicketEnclosureId": "g5u6m3xew6hxy",
                    "TicketEnclosureName": "Sala 1",
                    "TicketEnclosureConditions": "Enclosure conditions",
                    "TypeOfPersonDefinitionTypeChild": 2,
                    "TypeOfPersonDefinitionValueChild": 120,
                    "TypeOfPersonDefinitionTypeSenior": 1,
                    "TypeOfPersonDefinitionValueSenior": 65,
                    "Sessions": 
                    {
                        "SessionsGroupSessionContents": 
                        [
                            {
                                "SessionsGroupId": "7q59grjg1tuxw",
                                "SessionContentId": "fiajih99h79ak"
                            }, 
                            {
                                "SessionsGroupId": "8o9tskd4szqgs",
                                "SessionContentId": "m6noaxhzr33an"
                            },
                            {
                                "SessionsGroupId": "i73hiypge5576",
                                "SessionContentId": "suefs1zzn5ser"
                            }
                        ],
                        "SessionSessionContents": []
                    }
                },
                {
                    "TicketEnclosureId": "geu773xaqzh18",
                    "TicketEnclosureName": "Enclosure 2",
                    "TicketEnclosureConditions": "Enclosure 2 conditions",
                    "TypeOfPersonDefinitionTypeChild": 2,
                    "TypeOfPersonDefinitionValueChild": 120,
                    "TypeOfPersonDefinitionTypeSenior": 1,
                    "TypeOfPersonDefinitionValueSenior": 65
                }
            ],
            "ProductBases": 
            [
                {
                    "ProductBaseId": "gfo753rgjfbw6",
                    "ProductBaseName": "Entradas",
                    "ProductBaseDescription": "No se permiten cambios ni devoluciones.",
                    "DaysWithLimitedCapacity": "2022-11-01",
                    "Products": 
                    [
                        {
                            "ProductId": "ctgyir9m9q4bo",
                            "ProductName": "Entrada Adulto",
                            "ProductDescription": "Entrada para mayores de 12 años.",
                            "ProductInternalConsiderations": "Consideraciones internas",
                            "ProductCancellationConditions": "Condiciones de cancelación",
                            "CancellationPolicy": 
                            {
                                "IsRefundable": true,
                                "Rules": 
                                [
                                    {
                                        "HoursInAdvanceOfAccess": 6,
                                        "Percentage": 80
                                    }
                                ]
                            },
                            "DaysWithLimitedCapacity": "",
                            "HoursInAdvanceOfPurchase": 4,
                            "MinimumNumberByTransaction": 1,
                            "NumberOfPeople": 1,
                            "NumberOfAdults": 1,
                            "NumberOfBabies": 1,
                            "NumberOfChildren": 0,
                            "NumberOfSenior": 0,
                            "NumberOfGeneric": 0,
                            "ValidDates": 1,
                            "ValidDatesType": 0,
                            "AccessDateCriteria": 0,
                            "PricesAndDates": 
                            [
                                {
                                    "Price": "20",
                                    "Currency": "€",
                                    "CurrencyName": "Euro",
                                    "Dates": "2022-01-01,2022-01-02,2022-01-03,2022-07-31"
                                }, 
                                {
                                    "Price": "30",
                                    "Currency": "€",
                                    "CurrencyName": "Euro",
                                    "Dates": "2022-08-01,2022-08-02,2022-08-31"
                                }, 
                                {
                                    "Price": "15",
                                    "Currency": "€",
                                    "CurrencyName": "Euro",
                                    "Dates": "2022-09-01,2022-09-02,2022-12-31"
                                }
                            ],
                            "SalesDocumentSettingsViewModel":
                            {
                                "ShowPrice": true
                            },
                            "Tickets": 
                            [
                                {
                                    "TicketId": "1tqgtrf7ctefc",
                                    "IsQuotaTicket": true,
                                    "TicketName": "Ticket Adulto",
                                    "TicketEnclosureId": "geu773xaqzh18"
                                }
                            ]
                        }, 
                        {
                            "ProductId": "htgy4tgm9q21n",
                            "ProductName": "Entrada 3x2",
                            "ProductDescription": "Por cada dos adultos, entra un niño gratis.",
                            "DaysWithLimitedCapacity": "2022-04-17,2022-08-15",
                            "HoursInAdvanceOfPurchase": 4,
                            "MinimumNumberByTransaction": 1,
                            "NumberOfPeople": 3,
                            "NumberOfAdults": 2,
                            "NumberOfChildren": 1,
                            "NumberOfSenior": 0,
                            "NumberOfGeneric": 0,
                            "ValidDates": 1,
                            "ValidDatesType": 0,
                            "AccessDateCriteria": 1,
                            "PricesAndDates": 
                            [
                                {
                                    "Price": "35",
                                    "Currency": "€",
                                    "CurrencyName": "Euro",
                                    "Dates": "2022-01-01,2022-01-02,2022-01-03,2022-07-31"
                                }, 
                                {
                                    "Price": "50",
                                    "Currency": "€",
                                    "CurrencyName": "Euro",
                                    "Dates": "2022-08-01,2022-08-02,2022-08-31"
                                }, 
                                {
                                    "Price": "25",
                                    "Currency": "€",
                                    "CurrencyName": "Euro",
                                    "Dates": "2022-09-01,2022-09-02,2022-12-31"
                                }
                            ],
                            "SalesDocumentSettingsViewModel":
                            {
                                "ShowPrice": true
                            },
                            "Tickets": 
                            [
                                {
                                    "TicketId": "1tqgtrf7ctefc",
                                    "IsQuotaTicket": true,
                                    "TicketName": "Ticket Adulto",
                                    "TicketConditions": "Ticket conditions",
                                    "TicketEnclosureId": "geu773xaqzh18",
                                    "FromAccessDay": 1,
                                    "ToAccessDay": 1,
                                    "TicketsQuestionsProfileId": "MyProfilesQuestions"
                                }, 
                                {
                                    "TicketId": "2lob55g8w3fff",
                                    "IsQuotaTicket": true,
                                    "TicketName": "Ticket Adulto segundo día",
                                    "TicketConditions": "Ticket conditions",
                                    "TicketEnclosureId": "geu773xaqzh18",
                                    "FromAccessDay": 2,
                                    "ToAccessDay": 2
                                }, 
                                {
                                    "TicketId": "jkp78j40cnfh3",
                                    "IsQuotaTicket": true,
                                    "TicketName": "Ticket Niño",
                                    "TicketEnclosureId": "geu773xaqzh18",
                                    "FromAccessDay": 1,
                                    "ToAccessDay": 1
                                }, 
                                {
                                    "TicketId": "gggsijt911am4",
                                    "IsQuotaTicket": true,
                                    "TicketName": "Ticket Niño segundo día",
                                    "TicketEnclosureId": "geu773xaqzh18",
                                    "FromAccessDay": 2,
                                    "ToAccessDay": 2
                                }
                            ]
                        }, 
                        {
                            "ProductId": "q2oghu9mye7h2",
                            "ProductName": "Película de animación 3D",
                            "ProductDescription": "Película de animación para descansar de atracciones",
                            "DaysWithLimitedCapacity": "",
                            "HoursInAdvanceOfPurchase": 4,
                            "MinimumNumberByTransaction": 1,
                            "NumberOfPeople": 1,
                            "NumberOfAdults": 0,
                            "NumberOfChildren": 0,
                            "NumberOfSenior": 0,
                            "NumberOfGeneric": 1,
                            "ValidDates": 1,
                            "ValidDatesType": 0,
                            "AccessDateCriteria": 0,
                            "PricesAndDates": 
                            [
                                {
                                    "Price": "5",
                                    "Currency": "€",
                                    "CurrencyName": "Euro",
                                    "Dates": "2022-01-01,2022-01-02,2022-01-03,2022-12-31"
                                }
                            ],
                            "SalesDocumentSettingsViewModel":
                            {
                                "ShowPrice": false
                            },
                            "Tickets": 
                            [
                                {
                                    "TicketId": "fb8mcqxyo22rg",
                                    "IsQuotaTicket": true,
                                    "TicketName": "Entrada 3D",
                                    "TicketEnclosureId": "g5u6m3xew6hxy"
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ]
}
```
