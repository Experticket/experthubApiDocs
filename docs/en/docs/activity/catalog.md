# Activities catalog

The first step will be to get the complete catalog of providers, categories (productBases) and products for its internal processing.

The information in the catalog includes unique identifiers for Provider, Product and Ticket, which will subsequently be used to create a sale.

It will also include other data such as product price, depending on the dates, or the product’s commercial terms.

Continuing with our example, it could be the case that the provider PAC’s "2x1 Children’s Ticket” product price drops and prolongs the sale’s validity.

## Access method

**POST** /activity/catalog

## Request data structure

We can filter the catalog result using different filters in the request's body.

Each filter will be considered an ***AND***. For example, several *ProductIds* from different providers may be filtered, but it would not make sense to filter by a *ProviderId* and a *ProductId* not belonging to this *ProviderId*.

- **`ProviderIds`**: provider identifiers list.
- **`ProductBaseIds`**: list category identifiers.
- **`ProductIds`**: product identifiers list.
- **`FromDate`**: start date. Does not allow values less than the current day. *ISO 8601 format (yyyy-MM-dd)*.
- **`ToDate`**: ending date. By default, its value is that of the date corresponding to a year from now. *ISO 8601 format (yyyy-MM-dd)*.
- **`ReferenceDate`**: requires that the day that is taken as a reference for the calculation of prices and availability is not today, but the indicated one. For example it will be used if the prices change depending on the days left until the date of entry. *ISO 8601 format (yyyy-MM-dd)*
- **`LanguageCode`**: sets the language in which to display the catalog’s text (name, description, provider conditions, product, etc.). By default it shall return to the language configured for the partner. *ISO format 639-1*.
- **`ShowProductsOutOfActiveDateRange`**: when it is `#!csharp true`, the response will return products where today (or the day indicated in `ReferenceDate`) is outside of their sale date range. For example, if it is December and there are products that can be sold from January, setting this value to true will allow us to discover that those products exist.

### Request example

--8<-- "includes/examples/activity/catalogQueryExamples.md"

## Response data structure

- **`LastUpdatedDateTime`**: last catalog modification date. *ISO 8601 format (yyyy-MM-ddThh:mm:ss.fffffff)*.
- **`Providers`**: providers array.
    - **`ProviderId`**: provider identifier. Alphanumeric of 13 characters.
    - **`ProviderName`**: provider name.
    - **`ProviderDescription`**: provider description.
    - **`ProviderCommercialConditions`**: provider comercial terms. This field will not be displayed if it is not defined.
    - **`ProviderAccessConditions`**: provider access conditions. This field will not be displayed if it is not defined.
    - **`ExchangeVoucherPoint`**: place where the tickets can be used or exchabge.
    - **`AdvancedDateSelectorMethodName`**: name of the method that determines if product tickets can have their own access date.

        ??? example "Possible values"
            --8<-- "includes/annex/advancedDateSelector.en.md"

    - **`CancellationPolicy`**: describe the cancellation policies that apply when canceling a sale from this provider. If a specific product does not have cancellation policies these will apply.
        - **`IsRefundable`**: indicates if the customer can cancel for free at some point in time.
        - **`Rules`**: rules that apply when canceling.
            - **`HoursInAdvanceOfAccess`**: indicates the number of hours in advance regarding the access date from which the cancellation fee set in `Percentage` will be applied.
            - **`Percentage`**: percentage of the total product amount that won't be refunded in case of cancellation.
    - **`DemandAccessDate`**: indicates whether the access date is needed. If it is not necessary, when adding the product to the cart, the date of purchase must be used.
    - **`TaxType`**: indicates the type of tax on the provider's products.

        ??? example "Possible values"
            - 0: IVA
            - 1: IGIC

    - **`Type`**: indicates the type of provider. By default is 0.

        ??? example "Possible values"
            - 0: Activity
            - 1: Accommodation
            - 2: Transport

    - **`PurchaseFlowType`**: indicates the sale flow. It can be used to know if the tickets and the access codes are going to be accsibles instantly or if require some processing.

        ??? example "Possible values"
            - 1: Open sale.
            - 2: Requires processing by the provider.

    - **`IsForGroups`**: indicates if the provider's products are intended for sale to groups.
    - **``IsForSeasonTickets``**: indicates if the provider's products are season tickets.
    - **`LimitOfNumberOfPeopleToBeGroup`**: limits the number of people that make up a product from which the sale is considered for "groups". For example, if this limit is "19" and the provider is not for groups (`#!csharp IsForGroups == false`), sales with 20 or more people will not be accepted. On the contrary, if the provider is for groups (`#!csharp IsForGroups == true`), sales for 20 or more people will only be accepted.
    - **`Logo`**: url to download the provider's logo.
    - **`Location`**: location information.
        - **`CountryCode`**: country code (es, fr...).
        - **`City`**: city.
        - **`Address`**: address.
        - **`ZipCode`**: postal code.
        - **`Lat`**: latitude.
        - **`Lng`**: longitude.
    - **`Ticket enclosures`**: provider enclosures information.
        - **`TicketEnclosureId`**: enclosure identifier.
        - **`TicketEnclosureName`**: enclosure name.
        - **`TicketEnclosureConditions`**: *optional*, enclosure conditions.
        - **`TypeOfPersonDefinitionTypeChild`**: *optional*, indicates which attribute applies to the person to consider him a child.

            ??? example "Possible values"
                --8<-- "includes/annex/typeOfPersonDefinition.en.md"

        - **`TypeOfPersonDefinitionValueChild`**: *optional*, indicates the value assigned to the type of person child.
        - **`TypeOfPersonDefinitionTypeAdult`**: *optional*, indicates which attribute applies to the person to consider him an adult.

            ??? example "Possible values"
                --8<-- "includes/annex/typeOfPersonDefinition.en.md"

        - **`TypeOfPersonDefinitionValueAdult`**: *optional*, indicates the value assigned to the type of person adult.
        - **`TypeOfPersonDefinitionTypeSenior`**: *optional*, indicates which attribute applies to the person to consider him a senior.

            ??? example "Possible values"
                --8<-- "includes/annex/typeOfPersonDefinition.en.md"

        - **`TypeOfPersonDefinitionValueSenior`**: *optional*, indicates the value assigned to the type of person senior.
        - **`Sessions`**: *optional*, defines the relationship between sessions and content. Before continuing, it is essential to study the [sessions section](sessions.md).
            - **`SessionContentProfileId`**: for more information about this identifier, see the [sessions page](sessions.md).
            - **`SessionGroupProfileId`**: for more information about this identifier, see the [sessions page](sessions.md).
            - **``HasSeating``**: indicates if the enclosure has seats, in which case it will be necessary to check the type of seat assignment at ticket level.
            - **`SessionsGroupSessionContents`**: defines the relationship between session groups and session contents. That is, all sessions in the session group will have the session content assigned. `SessionsGroupSessionContents` is exclusive with respect to `SessionSessionContents`.
                - **`SessionsGroupId`**: session group identifier.
                - **`SessionContentId`**: session content identifier.
            - **`SessionSessionContents`**: defines the relationship between sessions and session contents. `SessionSessionContents` is exclusive with respect to `SessionsGroupSessionContents`.
                - **`SessionId`**: session identifier.
                - **`SessionContentId`**: session content identifier.
                - **`SessionTime`**: session date and time.
                - **`HasLimitedCapacity`**: indicates if the session has limited capacity. If so, it will be essential to check the availability of the session before creating a sale. More information about it in [obtaining available capacity](availability.md).
            - **`TicketEnclosureAutoAssignSessionType`**: indicates which attribute is applied when choosing sessions. They can be self-assigned sessions by the system, eligible, or a mixture of the two cases.In the case of self-assigned sessions, you can check which sessions are going to be assigned before adding the product to the cart using the method to [check the auto-assigned session](autoAssignSession.md).

                ??? example "Possible values"
                    --8<-- "includes/annex/autoAssignSessionType.en.md"

        - **`ProductBases`**: categories array.
            - **`ProductBaseId`**: category identifier. 13 character alphanumeric.
            - **`ProductBaseName`**: category name.
            - **`ProductBaseDescription`**:  category description. It usually contains the conditions common to all its products.
            - **`DaysWithLimitedCapacity`**: fdates in which all the products in this category have a limited capacity. Therefore, it will be essential to check the availability of the category before creating a sale. The dates will be in *ISO 8601 format (yyyy-MM-dd)*, and will be separated from each other by a comma. More information about it in the section on [obtaining available capacity](availability.md).
            - **`LimitOfNumberOfPeopleToBeGroup`**: *optional*, same meaning as the `LimitOfNumberOfPeopleToBeGroup` property in the `Provider` node. If specified, the most restrictive between this value and that of the provider will be used.
            - **`Products`**: product array.
                - **`ProductId`**: product identifier. 13 character alphanumeric.
                - **`ProductName`**: product name.
                - **`SuggestedSalesProductName`**: suggested product name for sale.
                - **`ProductDescription`**: product description. It usually contains the conditions of the product.
                - **`ProductInternalConsiderations`**: internal considerations of the product that only the collaborator should know.

                    ???+ danger "Important"
                        **NEVER** show to end customer.

                - **`ProductCancellationConditions`**: cancellation conditions for the product.
                - **`CancellationPolicy`**: indicates the cancellation policies that apply when canceling a sale of this product. If this node is present, it takes precedence over the provider's `CancellationPolicy` node.
                    - **`IsRefundable`**: indicates if the customer can cancel for free at any time.
                    - **`Rules`**: rules that apply when making the cancellation.
                        - **`HoursInAdvanceOfAccess`**: indicates the number of hours in advance with respect to the access date from which the price penalty indicated in `Percentage` will be applied.
                        - **`Percentage`**: percentage of penalty on the ticket price.
                - **`StartIsActiveDate`**: *optional*, if it exists, it defines the date from which it is possible to sell the product.
                - **`EndIsActiveDate`**: *optional*, if it exists, it defines the date until which it is possible to sell the product.
                - **`DaysWithLimitedCapacity`**: dates in which the product has a limited capacity. Therefore, it will be essential to check the availability of the product before creating a sale. Dates will be in *ISO 8601 format (yyyy-MM-dd)*, and will be separated from each other by a comma. More information about it in the section on [obtaining available capacity](availability.md).
                - **`HoursInAdvanceOfPurchase`**: hours in advance of the purchase compared to 00:00 a.m. the day after the visit. For example, if a product has `HoursInAdvanceOfPurchase = 4`, and a customer makes a purchase for August 15, the time limit that the product has to be sold is 8:00 p.m. on August 15 itself (that is, 4 hours before 00:00 a.m. on August 16). This is important, for example, so that a customer does not buy the products for a day when the venue is already closed.
                - **`MaxHoursInAdvanceOfPurchase`**: *optional*, maximum hours in advance of the purchase compared to 00:00 a.m. the day after the visit. For example, if a product has `MaxHoursInAdvanceOfPurchase = 240`, and a customer makes a purchase for August 15, the product cannot be sold before August 6 (that is, 240 hours = 10 days before 00:00 a.m. on August 16). This is useful, for example, to limit the period of sale of a product to a period of days before.
                - **`MinimumNumberByTransaction`**: minimum number of products for each sale. Default is 1. For example, a product of the type "Entry ticket with discount starting from 3 products". In that case, MinimumNumberByTransaction would be 3.
                - **`NumberOfPeople`**: number of people who compute to consider a sale as a "group". That is, it computes for the limit `LimitOfNumberOfPeopleToBeGroup`.
                - **`NumberOfAdults`**: number of adults, included in the `NumberOfPeople` field.
                - **`NumberOfBabies`**: number of babies, included in the `NumberOfPeople` field.
                - **`NumberOfChildren`**: number of children, included in the `NumberOfPeople` field.
                - **`NumberOfSenior`**: number of seniors, included in the `NumberOfPeople` field.
                - **`NumberOfGeneric`**: number of generics, included in the `NumberOfPeople` field. It is a very useful field, for example, if a product is valid for both adults and children as well as for seniors.
                - **`RequiresRealTimePrice`**: indicates if the product requires real-time pricing.

                    ??? tip "Implications"
                        In case it is defined as `#!csharp true` it will be necessary before starting any sale to make the call to [check the price in real time](realTimePrices.md). Since the product price may be different depending on some criteria.

                - **`ValidDays`**: days of validity.
                - **`ValidDaysType`**: type of valid days.

                    ??? example "Possible values"
                        - 0: consecutive.
                        - 1: not consecutive.

                - **`PriceMode`**: indicate the type of price.

                    ??? example "Possible values"
                        - 1: RRP.
                        - 2: net price.

                - **`Commission`**: in case `PriceMode = RRP`, this indicates the commission.
                    - **`Type`**: indicates the type of commission applied.

                        ??? example "Possible values"
                            - 1: percentage.
                            - 2: absolute value.

                    - **`Value`**: value of that commission.

                        ??? info "Example"
                            - if `Type = 1` y `Value = 10`, indicates that the commission is 10% with respect to the `Price` of the product. That is, if the `Price` is equal to €100, the calculated commission would be €10.
                            - if `Type = 2` y `Value = 3`, indicates that the commission per product is €3.

                - **`AccessDateCriteria`**: indicates the criteria for the access date.

                    ??? example "Possible values"
                        --8<-- "includes/annex/accessDateCriteria.en.md"

                - **`BarcodeAssignment`**: *optional*, indicates what the barcode is to be assigned to.

                    ??? example "Possible values"
                        - 1: Ticket (default value if `BarcodeAssignment` is not defined).
                        - 2: Person.

                        ???+ info "Example"
                            The "Two day ticket" product consisting of one adult and 2 tickets (day 1 ticket, day 2 ticket):

                            - `BarcodeAssignment = Ticket`: each of the tickets will have its own barcode.
                            - `BarcodeAssignment = Person`: there will only be one barcode (shared by both tickets). A direct consequence of this case would be when printing a PDF with the tickets, since we would only have to print a PDF of the product, given that despite having two tickets there is only one barcode.

                - **`PricesAndDates`**: array of "*price and dates*". It has a double functionality. On the one hand, it defines what access dates the product is available for, and on the other hand, it defines what price applies to what dates.
                    - **`Price`**: price.
                    - **`Currency`**: currency.
                    - **`CurrencyName`**: name of currency.
                    - **`Dates`**: dates will be in *ISO 8601 format (yyyy-MM-dd)* and will be separated from each other by a comma.
                    - **`OriginalPrice`**: *optional*, price of the product before applying discounts if any.
                    - **`TaxBreakdown`**: array with the tax breakdown.
                        - **`TaxPercentage`**: tax percentage (out of 100).
                        - **`PriceWithoutTaxes`**: price without tax.
                        - **`PriceWithTaxes`**: price with taxes.
                - **`Release`**: *optional*, number of days in advance required for the customer to cancel the product at no cost.

                    ??? info "Example"
                        - 0: The client can cancel the day of entry to the park at no cost.
                        - 1: The client can cancel one day before the entrance to the park without cost.

                - **`SalesDocumentSettings`**: settings regarding the access document (PDF, passbook). This information will also come as a result when confirming a sale.

                    ??? tip "Advice"
                        If the documents generated by us are used, it will not be necessary to take these settings into account. Otherwise, you should take them into consideration.

                    - **`Disable`**: indicates if no access document will be generated for this product.
                    - **`ShowPrice`**: indicates if the price should be displayed in the access document.
                    - **`AccessDateCriteriaOpenDateSalesDocument`**: only in case `AccessDateCriteria == 1` (open date). Indicates what we must inform the client regarding the date of access.

                        ??? example "Possible values of AccessDateCriteria and AccessDateCriteriaOpenDateSalesDocument"
                            --8<-- "includes/annex/accessDateCriteria.en.md"

                - **`HasSaleFlowRule`**: indicates if the product has any associated sales flow rule. In the case of being ``#!csharp true``, it is recommended to consult the method [Check sale flow rules](checkSaleFlowRules.md) to check what changes the inclusion of this product will produce when adding it to the cart.
                - **`Tickets`**: *optional*, ticket array. In case the product does not work with tickets, this field will not exist.
                    - **`TicketId`**: ticket identifier. 13 character alphanumeric.
                    - **`IsQuotaTicket`**: boolean indicating whether or not the ticket is capacity type, which means that if `#!csharp true` the ticket will compute for the total capacity necessary to reserve the product. For example, if we have a product where it has 3 defined tickets but only 2 of them are capacity type, then when checking the availability for this product we must take into account that at the capacity level it needs 2 availability. In other words, if the available capacity was 1, we could not reserve this product. More information about it in the section on [obtaining available capacity](availability.md).
                    - **`TicketName`**: ticket name.
                    - **`TicketConditions`**: *optional*, ticket conditions.
                    - **`TicketEnclosureId`**: identifier of the enclosure to which the ticket belongs. Several tickets can belong to the same enclosure.
                    - **``SeatingAssignType``**: Indicates the type of seat assignment that applies.

                        ??? example "Possible values"
                            - 1: **Auto assigned**, seats will be automatically assigned by the system.
                            - 3: **Processing required**, the seats will be assigned later by the provider.

                    - **`FromAccessDay`** and **`ToAccessDay`**: if they are defined, they indicate for which days with respect to the first date of access the ticket is valid.

                        ???+ tip "Advice"
                            The result of the call to confirm a sale already gives us the range of access dates for each ticket. So it's entirely feasible not to handle `FromAccessDay` and `ToAccessDay` and rely on what that call returns.

                        ??? info "Example"

                            - If the ticket defines FromAccessDay = 1 and ToAccessDate = 1, the client must use it on the first day of access.
                            - If the ticket defines FromAccessDay = 2 and ToAccessDate = 2, the client must use it on the second day of access.
                            - If the ticket defines FromAccessDay = 1 and ToAccessDate = 2, the customer will be able to enter on either the first or second day.
                            - If the ticket defines FromAccessDay = 2 and ToAccessDate is not defined, the client will be able to enter from the second day to an indefinite day, for example until the end of the season, *unless the product conditions indicate otherwise*.
                            - If the ticket does not define either FromAccessDay or ToAccessDate, the customer will only be able to enter on the first day, *unless the product conditions indicate otherwise*.

                    - **`TypeOfPerson`**: *optional*, defines the type of person and their numbering.
                        - **`Type`**: indicates the type of person.

                            ??? example "Possible values"
                                - 1: Baby
                                - 2: Child
                                - 3: Adult
                                - 4: Senior
                                - 5: Generic

                        - **`PersonNumber`**: identifier of the person number by type.

                        ??? example "Example"
                            - "3x2 Ticket" product made up of two adults and one child and defined by three tickets:
                                - Adult Ticket: adult 1 (Type = 3, PersonNumber = 1)
                                - Adult Ticket: adult 2 (Type = 3, PersonNumber = 2)
                                - Child Ticket: child 1 (Type = 2, PersonNumber = 1)
                            - Product "2x1 ticket plus second consecutive day" consisting of two adults and 4 tickets:
                                - Adult First Day Ticket: adult 1 (Type = 3, PersonNumber = 1)
                                - Adult First Day Ticket: adult 2 (Type = 3, PersonNumber = 2)
                                - Second Day Adult Ticket: adult 1 (Type = 3, PersonNumber = 1)
                                - Second Day Adult Ticket: adult 2 (Type = 3, PersonNumber = 2)

                    - **``RequiresDeliveryManagement``**: indicates if it is a ticket that requires physical delivery. If so, you will have to choose the delivery method when adding the product to the cart. You can check the available delivery methods in the section [Get Delivery Methods](deliveryMethods.md).

                - **`ProductPaxGroupingId`**: *optional*, identifier of the product group to which the product belongs.

        - **`ProductPaxGroupings`**: groupings of products whose main difference is the people who compose it.
            - **`ProductPaxGroupingId`**: grouping identifier. 13 character alphanumeric.
            - **`ProductPaxGroupingName`**: name of the grouping.

    - **`Urls`**: *optional*, array of urls to access the provider's ticketshop page. Only in the case of having personalized DNS.
        - **`LanguageCode`**: code of the language with which it is going to be accessed. Represented by the *ISO format 639-1*.
        - **`Url`**: access url.

- **`CombinedProducts`**: array of combined products.
    - **`CombinedProductId`**: combined product identifier.
    - **`Name`**: combined product name.
    - **`PriceFrom`**: price "*from*" for the combined product.
    - **`PriceTo`**: price "*to*" for combined product.
    - **`Products`**: array of products that are part of the combined product.
        - **`ProductId`**: product identifier.
    - **`RequiresRealTimePrice`**: indicates if you need to consult the price in real time for the combined product. See [obtaining the price in real time](realTimePrices.md)
- **`PartnerSettings`**: shows the partner settings.
    - **`DemandClientData`**: boolean `#!csharp true/false` that indicates if is mandatory to tell the client information when sale confirmation is done.
    - **`EnableCancellationRequest`**:  boolean `#!csharp true/false` taht indicates if Test It is allowed to request cancellations via API.
    - **`PaymentType`**: indicates the payment type for the partner.

        ??? example "Possible values"
            - 1: Debit
            - 2: Credit
            - 3: Credit, except for groups
            - 4: Prepaid

- **`Success`**: boolean, `#!csharp true/false` that indicates if the obtaining of the catalog has been successful or not.
- **`Timestamp`**: time of obtaining the catalog. *ISO 8601 format (yyyy-MM-ddThh:mm:ss.fffffff)*.
- **`ErrorMessage`**: error message explaining why the catalog fetch was unsuccessful. If it was correct, it will return `#!csharp null`.

### Response example

--8<-- "includes/examples/activity/catalogResponseExamples.md"
