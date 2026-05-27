# Activities catalog

The first step will be to get the complete catalog of providers, categories (productBases) and products for its internal processing.

The information in the catalog includes unique identifiers for Provider, Product and Ticket, which will subsequently be used to create a sale.

It will also include other data such as product price, depending on the dates, or the product’s commercial terms.

!!! caution "Misuse of the API"
    A misuse of this call could be to perform a query with each sale, the correct use must be to store and process locally and consult periodically the [date of the last modification of the catalog](lastCatalogUpdatedDate.md). Only in the event that this date of modification is later than the one obtained in the catalog must we obtain the catalog again.

## Access method

**POST** /activity/catalog

## Request structure

We can filter the catalog result using different filters in the request's body.

Each filter will be considered an ***AND***. For example, several *ProductIds* from different providers may be filtered, but it would not make sense to filter by a *ProviderId* and a *ProductId* not belonging to this *ProviderId*.

- **`ProviderIds`**: (``list``) ``Optional``. Provider identifier list.
    - **``(string)``**: ``Optional``. Provider identifier.
- **`ProductBaseIds`**: (``list``) ``Optional``. Category identifier list.
    - **``(string)``**: ``Optional``. ProductBase identifier.
- **`ProductIds`**: (``list``) ``Optional``. Product identifier list.
    - **``(string)``**: ``Optional``. Product identifier.
- **`FromDate`**: (``date``) ``Optional``. Start date. Does not allow values less than the current day. *ISO 8601 format (yyyy-MM-dd)*.
- **`ToDate`**: (``date``) ``Optional``. Ending date. By default, its value is that of the date corresponding to a year from now. *ISO 8601 format (yyyy-MM-dd)*.
- **`ReferenceDate`**: (``date``) ``Optional``. Requires that the day that is taken as a reference for the calculation of prices and availability is not today, but the indicated one. For example it will be used if the prices change depending on the days left until the date of entry. *ISO 8601 format (yyyy-MM-dd)*
- **`LanguageCode`**: (``string``) ``Optional``. Sets the language in which the catalog texts will be displayed (name, description, provider conditions, product, etc.). By default, the language configured for the partner will be returned. *ISO 639-1 format*.
- **`ShowProductsOutOfActiveDateRange`**: (``boolean``) ``Optional``. When it is `#!csharp true`, the response will return products where today (or the day indicated in `ReferenceDate`) is outside of their sale date range. For example, if it is December and there are products that can be sold from January, setting this value to true will allow us to discover that those products exist.

### Request examples

--8<-- "includes/examples/activity/catalogQueryExamples.md"

## Response structure

- **`LastUpdatedDateTime`**: (``dateTime``). Last catalog modification date. *ISO 8601 format (yyyy-MM-ddThh\:mm\:ss.fffffff)*.
- **`Providers`**: (``list``). Providers array.
    - **`ProviderId`**: (``string``). Provider identifier. Alphanumeric of 13 characters.
    - **`ProviderName`**: (``string``). Provider name.
    - **`ProviderDescription`**: (``string``). Provider description.
    - **`ProviderCommercialConditions`**: (``string``) ``Optional``. Provider commercial terms. This field will not be displayed if it is not defined.
    - **`ProviderAccessConditions`**: (``string``) ``Optional``. Provider access conditions. This field will not be displayed if it is not defined.
    - **`ExchangeVoucherPoint`**: (``string``) ``Optional``. Place where the tickets can be used or exchanged.
    - **`AdvancedDateSelectorMethodName`**: (``string``) ``Optional``. Name of the method that determines if product tickets can have their own access date.

        ??? example "Possible values"
            --8<-- "includes/annex/advancedDateSelector.en.md"

    - **`CancellationPolicy`**: (``object``) ``Optional``. Indicates the cancellation policies that apply when canceling a sale from this provider. If a specific product does not have cancellation policies, these will apply.
        - **`IsRefundable`**: (``boolean``). Indicates if the customer can cancel for free at some point in time.
        - **`Rules`**:  (``list``). Rules that apply when making the cancellation.
            - **``(object)``**: cancellation ranges.
                - **`HoursInAdvanceOfAccess`**: (``decimal``). Indicates the number of hours in advance regarding the access date from which the cancellation fee set in `Percentage` will be applied.
                - **`Percentage`**: (``decimal``). Penalty percentage on the ticket price.
    - **`DemandAccessDate`**: (``boolean``). Indicates whether the access date is needed. If it is not necessary, when adding the product to the cart, the date of purchase must be used.
    - **`TaxType`**: (``byte``). Indicates the type of tax on the provider's products.

        ??? example "Possible values"
            - 0: IVA
            - 1: IGIC

    - **`Type`**: (``byte``). Indicates the type of provider. By default is 0.

        ??? example "Possible values"
            - 0: Activity
            - 1: Accommodation
            - 2: Transport

    - **`DemandAccessDateOnOpenDate`**: (``boolean``). If the product is open dated, this parameter determines, with true or false, whether access dates must be requested.

    - **`PurchaseFlowType`**: (``byte``). Indicates the provider's sale flow type. It is used to know whether the tickets and access codes will be available at the time of purchase or later.

        ??? example "Possible values"
            - 1: Open sale.
            - 2: Requires processing by the provider.

    - **`IsForGroups`**: (``boolean``). Indicates if the provider's products are intended for sale to groups.
    - **`IsForSeasonTickets`**: (``boolean``). Indicates if the provider's products are season tickets.
    - **`IsInsurable`**: (`boolean`) `Optional`. Indicates whether it is possible to add cancellation insurance for this product.

        ??? tip "Implications"
            If it is defined as `#!csharp true`, before starting any sale it will be necessary to make the call to [check available policies](checkInsurancePolicies.md). This function returns a list of available policies with their identifiers. If we want to add one of these policies to the sale, we will pass that policy identifier (`Id`) in the `InsurancePolicyId` property in the [reservation confirmation](../shoppingCart/sale.md).

    - **`LimitOfNumberOfPeopleToBeGroup`**: (``int``). Limits the number of people that make up a product from which the sale is considered for "groups". For example, if this limit is "19" and the provider is not for groups (`#!csharp IsForGroups == false`), sales with 20 or more people will not be accepted. On the contrary, if the provider is for groups (`#!csharp IsForGroups == true`), sales for 20 or more people will only be accepted.
    - **`Logo`**: (``string``). URL to download the provider's logo.
    - **`Tags`**: (``list``). Array of [tag identifiers](tags.md) applied to the provider.
        - **``(string)``**: tag identifier.
    - **`Location`**: (``object``). Location information.
        - **`CountryCode`**: (``string``). Country code (es, fr...).
        - **`City`**: (``string``). City.
        - **`Address`**: (``string``). Address.
        - **`ZipCode`**: (``string``). Postal code.
        - **`Lat`**: (``double``). Latitude.
        - **`Lng`**: (``double``). Longitude.
        - **`Region`**: (``string``). Region.
    - **`Ticket enclosures`**: (``list``). Provider enclosures information.
        - **`TicketEnclosureId`**: (``string``). Enclosure identifier.
        - **`TicketEnclosureName`**: (``string``). Enclosure name.
        - **`TicketEnclosureConditions`**: (``string``) ``Optional``. Enclosure conditions.
        - **`TypeOfPersonDefinitionTypeChild`**: (``byte``) ``Optional``. Indicates which attribute applies to the person to consider him a child.

            ??? example "Possible values"
                --8<-- "includes/annex/typeOfPersonDefinition.en.md"

        - **`TypeOfPersonDefinitionValueChild`**: (``decimal``) ``Optional``. Indicates the value assigned to the type of person child.
        - **`TypeOfPersonDefinitionTypeAdult`**: (``byte``) ``Optional``. Indicates which attribute applies to the person to consider him an adult.

            ??? example "Possible values"
                --8<-- "includes/annex/typeOfPersonDefinition.en.md"

        - **`TypeOfPersonDefinitionValueAdult`**: (``decimal``) ``Optional``. Indicates the value assigned to the type of person adult.
        - **`TypeOfPersonDefinitionTypeSenior`**: (``byte``) ``Optional``. Indicates which attribute applies to the person to consider him a senior.

            ??? example "Possible values"
                --8<-- "includes/annex/typeOfPersonDefinition.en.md"

        - **`TypeOfPersonDefinitionValueSenior`**: (``decimal``) ``Optional``. Indicates the value assigned to the type of person senior.
        - **`Sessions`**:  (``object``) ``Optional``. Defines the relationship between sessions and content. Before continuing, it is essential to study the [sessions section](sessions.md).
            - **`SessionContentProfileId`**: (``string``). For more information about this identifier, see the [sessions page](sessions.md).
            - **`SessionGroupProfileId`**: (``string``). For more information about this identifier, see the [sessions page](sessions.md).
            - **``HasSeating``**: (``boolean``). Indicates if the enclosure has seats, in which case it will be necessary to check the type of seat assignment at ticket level.
            - **`SessionsGroupSessionContents`**:  (``object``). Defines the relationship between session groups and session contents. That is, all sessions in the session group will have the session content assigned. `SessionsGroupSessionContents` is exclusive with respect to `SessionSessionContents`.
                - **`SessionsGroupId`**: (``string``). Session group identifier.
                - **`SessionContentId`**: (``string``). Session content identifier.
            - **`SessionSessionContents`**: (``list``). Defines the relationship between sessions and session contents. `SessionSessionContents` is exclusive with respect to `SessionsGroupSessionContents`.
                - **`SessionId`**: (``string``). Session identifier.
                - **`SessionContentId`**: (``string``). Session content identifier.
                - **`SessionTime`**: (``dateTime``). Session date and time.
                - **`HasLimitedCapacity`**: (``boolean``). Indicates if the session has limited capacity. If so, it will be essential to check the availability of the session before creating a sale. More information about it in [obtaining available capacity](availability.md).
            - **`TicketEnclosureAutoAssignSessionType`**: (``byte``). Indicates which attribute is applied when choosing sessions. They can be self-assigned sessions by the system, eligible, or a mixture of the two cases.In the case of self-assigned sessions, you can check which sessions are going to be assigned before adding the product to the cart using the method to [check the auto-assigned session](autoAssignSession.md).

                ??? example "Possible values"
                    --8<-- "includes/annex/autoAssignSessionType.en.md"

        - **`ProductBases`**: (``list``). Categories array.
            - **`ProductBaseId`**: (``string``). Category identifier. 13 character alphanumeric.
            - **`ProductBaseName`**: (``string``). Category name.
            - **`ProductBaseDescription`**: (``string``). Category description. It usually contains the conditions common to all its products.
            - **`LimitOfNumberOfPeopleToBeGroup`**: (``int``) ``Optional``. Same meaning as the `LimitOfNumberOfPeopleToBeGroup` property in the `Provider` node. If specified, the most restrictive between this value and that of the provider will be used.
            - **`IsInsurable`**: (`boolean`) `Optional`. Indicates whether it is possible to add cancellation insurance for this product.

                ??? tip "Implications"
                    If it is defined as `#!csharp true`, before starting any sale it will be necessary to make the call to [check available policies](checkInsurancePolicies.md). This function returns a list of available policies with their identifiers. If we want to add one of these policies to the sale, we will pass that policy identifier (`Id`) in the `InsurancePolicyId` property in the [reservation confirmation](../shoppingCart/sale.md).

            - **`Tags`**: (``list``). Array of [tag identifiers](tags.md) applied to the category.
                - **``(string)``**: tag identifier.
            - **`Products`**: (``list``). Product array.
                - **`ProductId`**: (``string``). Product identifier. 13 character alphanumeric.
                - **`ProductName`**: (``string``). Product name.
                - **`SuggestedSalesProductName`**: (``string``). Suggested product name for sale.
                - **`ProductDescription`**: (``string``). Product description. It usually contains the conditions of the product.
                - **`Tags`**: (``list``). Array of [tag identifiers](tags.md) applied to the product.
                    - **``(string)``**: Tag identifier.
                - **`ProductInternalConsiderations`**: (``string``). Internal considerations of the product that only the collaborator should know.

                    ???+ danger "Important"
                        **NEVER** show to end customer.

                - **`ProductCancellationConditions`**: (``string``). Cancellation conditions for the product.
                - **`CancellationPolicy`**: (``object``). Indicates the cancellation policies that apply when canceling a sale of this product. If this node is present, it takes precedence over the provider's `CancellationPolicy` node.
                    - **`IsRefundable`**: (``boolean``). Indicates if the customer can cancel for free at any time.
                    - **`Rules`**: (``list``). Rules that apply when making the cancellation.
                    - **``(object)``**: cancellation ranges.
                        - **`HoursInAdvanceOfAccess`**: (``decimal``). Indicates the number of hours in advance with respect to the access date from which the price penalty indicated in `Percentage` will be applied.
                        - **`Percentage`**: (``decimal``). Percentage of penalty on the ticket price.
                - **`StartIsActiveDate`**: (``dateTime``) ``Optional``. If it exists, it defines the date from which it is possible to sell the product.
                - **`EndIsActiveDate`**: (``dateTime``) ``Optional``. If it exists, it defines the date until which it is possible to sell the product.
                - **`DaysWithLimitedCapacity`**: (``string``). Dates in which the product has a limited capacity. Therefore, it will be essential to check the availability of the product before creating a sale. Dates will be in *ISO 8601 format (yyyy-MM-dd)*, and will be separated from each other by a comma. More information about it in the section on [obtaining available capacity](availability.md).
                - **`HoursInAdvanceOfPurchase`**: (``short``). Hours in advance of the purchase compared to 00:00 a.m. the day after the visit. For example, if a product has `HoursInAdvanceOfPurchase = 4`, and a customer makes a purchase for August 15, the time limit that the product has to be sold is 8:00 p.m. on August 15 itself (that is, 4 hours before 00:00 a.m. on August 16). This is important, for example, so that a customer does not buy the products for a day when the venue is already closed.
                - **`MaxHoursInAdvanceOfPurchase`**: (``dateTime``) ``Optional``. Maximum hours in advance of the purchase compared to 00:00 a.m. the day after the visit. For example, if a product has `MaxHoursInAdvanceOfPurchase = 240`, and a customer makes a purchase for August 15, the product cannot be sold before August 6 (that is, 240 hours = 10 days before 00:00 a.m. on August 16). This is useful, for example, to limit the period of sale of a product to a period of days before.
                - **`MinimumNumberByTransaction`**: (``int``). Minimum number of products for each sale. Default is 1. For example, a product of the type "Entry ticket with discount starting from 3 products". In that case, MinimumNumberByTransaction would be 3.
                - **`NumberOfPeople`**: (``int``). Number of people who compute to consider a sale as a "group". That is, it computes for the limit `LimitOfNumberOfPeopleToBeGroup`.
                - **`NumberOfAdults`**: (``byte``). Number of adults, included in the `NumberOfPeople` field.
                - **`NumberOfBabies`**: (``byte``). Number of babies, included in the `NumberOfPeople` field.
                - **`NumberOfChildren`**: (``byte``). Number of children, included in the `NumberOfPeople` field.
                - **`NumberOfSenior`**: (``byte``). Number of seniors, included in the `NumberOfPeople` field.
                - **`NumberOfGeneric`**: (``byte``). Number of generics, included in the `NumberOfPeople` field. It is a very useful field, for example, if a product is valid for both adults and children as well as for seniors.
                - **`RequiresRealTimePrice`**: (``boolean``). Indicates if the product requires real-time pricing.

                    ??? tip "Implications"
                        In case it is defined as `#!csharp true` it will be necessary before starting any sale to make the call to [check the price in real time](realTimePrices.md). Since the product price may be different depending on some criteria.

                - **`CanOnlyBeSoldAsPartOfCombinedProduct`**: (``boolean``) `Optional`. If `#!csharp true`, the product cannot be sold on its own, but it can be sold as part of at least one **`CombinedProduct`** available in the current query.

                - **`IsInsurable`**: (`boolean`) `Optional`. Indicates whether it is possible to add cancellation insurance for this product.

                    ??? tip "Implications"
                        If it is defined as `#!csharp true`, before starting any sale it will be necessary to make the call to [check available policies](checkInsurancePolicies.md). This function returns a list of available policies with their identifiers. If we want to add one of these policies to the sale, we will pass that policy identifier (`Id`) in the `InsurancePolicyId` property in the [reservation confirmation](../shoppingCart/sale.md).

                - **``IsForPackaging``**: (``boolean``). Indicates if the product has to be packaged, e.g. with an accommodation.
                - **`ValidDays`**: (``int``). Days of validity.
                - **`ValidDaysType`**: (``byte``). Type of valid days.

                    ??? example "Possible values"
                        - 0: consecutive.
                        - 1: not consecutive.

                - **`PriceMode`**: (``byte``). Indicate the type of price.

                    ??? example "Possible values"
                        - 1: Retail price.
                        - 2: net price.

                - **`Commission`**: (``list``). In case `PriceMode = Retail price`, this indicates the commission.
                    - **`Type`**: (``int``). Indicates the type of commission applied.

                        ??? example "Possible values"
                            - 1: percentage.
                            - 2: absolute value.

                    - **`Value`**: (``decimal``). Value of that commission.

                        ??? info "Example"
                            - if `Type = 1` y `Value = 10`, indicates that the commission is 10% with respect to the `Price` of the product. That is, if the `Price` is equal to €100, the calculated commission would be €10.
                            - if `Type = 2` y `Value = 3`, indicates that the commission per product is €3.

                - **`AccessDateCriteria`**: (``byte``). Indicates the criteria for the access date.

                    ??? example "Possible values"
                        --8<-- "includes/annex/accessDateCriteria.en.md"

                - **`BarcodeAssignment`**: (``byte``) ``Optional``. Indicates what the barcode is to be assigned to.

                    ??? example "Possible values"
                        - 1: Ticket (default value if `BarcodeAssignment` is not defined).
                        - 2: Person.

                        ???+ info "Example"
                            The "Two day ticket" product consisting of one adult and 2 tickets (day 1 ticket, day 2 ticket):

                            - `BarcodeAssignment = Ticket`: each of the tickets will have its own barcode.
                            - `BarcodeAssignment = Person`: there will only be one barcode (shared by both tickets). A direct consequence of this case would be when printing a PDF with the tickets, since we would only have to print a PDF of the product, given that despite having two tickets there is only one barcode.

                - **`PricesAndDates`**: (``list``). Array of "*price and dates*". It has a double functionality. On the one hand, it defines what access dates the product is available for, and on the other hand, it defines what price applies to what dates.
                    - **`Price`**: (``decimal``). Price.
                    - **`Currency`**: (``string``). Currency.
                    - **`CurrencyName`**: (``string``). Name of currency.
                    - **`Dates`**: (``string``). Dates will be in *ISO 8601 format (yyyy-MM-dd)* and will be separated from each other by a comma.
                    - **`OriginalPrice`**:  (``decimal``) ``Optional``. Price of the product before applying discounts if any.
                    - **`TaxBreakdown`**: (``list``). Array with the tax breakdown.
                        - **`TaxPercentage`**: (``decimal``). Tax percentage (out of 100).
                        - **`PriceWithoutTaxes`**: (``decimal``). Price without tax.
                        - **`PriceWithTaxes`**: (``decimal``)  price with taxes.
                - **`Release`**: (``short``) ``Optional``. Number of days in advance required for the customer to cancel the product at no cost.

                    ??? info "Example"
                        - 0: The client can cancel the day of entry to the park at no cost.
                        - 1: The client can cancel one day before the entrance to the park without cost.

                - **`SalesDocumentSettings`**: (``object``). Settings regarding the access document (PDF, passbook). This information will also come as a result when confirming a sale.

                    ??? tip "Advice"
                        If the documents generated by us are used, it will not be necessary to take these settings into account. Otherwise, you should take them into consideration.

                    - **`Disable`**: (``boolean``). Indicates if no access document will be generated for this product.
                    - **`ShowPrice`**: (``boolean``). Indicates if the price should be displayed in the access document.
                    - **`AccessDateCriteriaOpenDateSalesDocument`**: (``int``) ``Optional``. Only in case `AccessDateCriteria == 1` (open date). Indicates what we must inform the client regarding the date of access.

                        ??? example "Possible values of AccessDateCriteria and AccessDateCriteriaOpenDateSalesDocument"
                            --8<-- "includes/annex/accessDateCriteria.en.md"

                - **`HasSaleFlowRules`**: (``boolean``). Indicates if the product has any associated sales flow rule. In the case of being ``#!csharp true``, it is recommended to consult the method [Check sale flow rules](checkSaleFlowRules.md) to check what changes the inclusion of this product will produce when adding it to the cart.
                - **`Tickets`**: (``list``) ``Optional``. Ticket array. In case the product does not work with tickets, this field will not exist.
                    - **`TicketId`**: (``string``). Ticket identifier. 13 character alphanumeric.
                    - **`IsQuotaTicket`**: (``boolean``). Boolean indicating whether or not the ticket is capacity type, which means that if `#!csharp true` the ticket will compute for the total capacity necessary to reserve the product. For example, if we have a product where it has 3 defined tickets but only 2 of them are capacity type, then when checking the availability for this product we must take into account that at the capacity level it needs 2 availability. In other words, if the available capacity was 1, we could not reserve this product. More information about it in the section on [obtaining available capacity](availability.md).
                    - **`TicketName`**: (``string``). Ticket name.
                    - **`TicketConditions`**: (``string``) ``Optional``. Ticket conditions.
                    - **`TicketEnclosureId`**: (``string``). Identifier of the enclosure to which the ticket belongs. Several tickets can belong to the same enclosure.
                    - **``SeatingAssignType``**: (``byte``). Indicates the type of seat assignment that applies.

                        ??? example "Possible values"
                            - 1: **Auto assigned**, seats will be automatically assigned by the system.
                            - 3: **Processing required**, the seats will be assigned later by the provider.

                    - **`TicketsQuestionsProfileId`**: (``string``)  question profile identifier.
                    - **`FromAccessDay`** and **`ToAccessDay`**: if they are defined, they indicate for which days with respect to the first date of access the ticket is valid.

                        ???+ tip "Advice"
                            The result of the call to confirm a sale already gives us the range of access dates for each ticket. So it's entirely feasible not to handle `FromAccessDay` and `ToAccessDay` and rely on what that call returns.

                        ??? info "Example"

                            - If the ticket defines FromAccessDay = 1 and ToAccessDate = 1, the client must use it on the first day of access.
                            - If the ticket defines FromAccessDay = 2 and ToAccessDate = 2, the client must use it on the second day of access.
                            - If the ticket defines FromAccessDay = 1 and ToAccessDate = 2, the customer will be able to enter on either the first or second day.
                            - If the ticket defines FromAccessDay = 2 and ToAccessDate is not defined, the client will be able to enter from the second day to an indefinite day, for example until the end of the season, *unless the product conditions indicate otherwise*.
                            - If the ticket does not define either FromAccessDay or ToAccessDate, the customer will only be able to enter on the first day, *unless the product conditions indicate otherwise*.

                    - **`TypeOfPerson`**: (``list``) ``Optional``. Defines the type of person and their numbering.
                        - **`Type`**:  (``byte``). Indicates the type of person.

                            ??? example "Possible values"
                                - 1: Baby
                                - 2: Child
                                - 3: Adult
                                - 4: Senior
                                - 5: Generic

                        - **`PersonNumber`**: (``byte``). Identifier of the person number by type.

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

                    - **``RequiresDeliveryManagement``**: (``boolean``). Indicates if it is a ticket that requires physical delivery. If so, you will have to choose the delivery method when adding the product to the cart. You can check the available delivery methods in the section [Get Delivery Methods](deliveryMethods.md).

                - **`ProductPaxGroupingId`**: (``string``) ``Optional``. Identifier of the product group to which the product belongs.

        - **`ProductPaxGroupings`**: (``list``). Groupings of products whose main difference is the people who compose it.
            - **`ProductPaxGroupingId`**: (``string``). Grouping identifier. 13 character alphanumeric.
            - **`ProductPaxGroupingName`**: (``string``). Name of the grouping.

    - **`Urls`**: (``list``) ``Optional``. Array of URLs to access the provider's ticket office page. Only when using custom DNS.
        - **`LanguageCode`**: (``string``). Code of the language with which it is going to be accessed. Represented by the *ISO format 639-1*.
        - **`Url`**: (``string``). Access URL.

- **`CombinedProducts`**: (``list``). Array of combined products.
    - **`CombinedProductId`**: (``string``). Combined product identifier.
    - **`Name`**: (``string``). Combined product name.
    - **`PriceFrom`**: (``decimal``). Price "*from*" for the combined product.
    - **`PriceTo`**: (``decimal``). Price "*to*" for combined product.
    - **`Products`**: (``list``). Array of products that are part of the combined product.
        - **`ProductId`**: (``string``). Product identifier.
    - **`RequiresRealTimePrice`**: (``boolean``). Indicates if you need to consult the price in real time for the combined product. See [obtaining the price in real time](realTimePrices.md)
- **`SaleFlowRules`**: (``object``).
    - **`HasSaleFlowRules`**: (``boolean``). Indicates whether there are products with any associated sale flow rule. If it is `#!csharp true`, it is recommended to consult the [Check sale flow rules](checkSaleFlowRules.md) method to check what changes adding this product to the cart will produce.
    - **`ProductIdsWithSaleFlowRules`**: (``list``). Array of product identifiers. Indicates which catalog products have any associated sale flow rule.
    - **`DynamicProviderIdsWithSaleFlowRules`**: (``list``). Array of dynamic provider identifiers. Indicates which dynamic catalog providers have any associated sale flow rule.
- **`PartnerSettings`**: (``object``). Shows the partner settings.
    - **`DemandClientData`**: (``boolean``). Boolean `#!csharp true/false` that indicates if is mandatory to tell the client information when sale confirmation is done.
    - **`DemandClientTaxData`**: (``boolean``). Boolean `#!csharp true/false` that indicates if is mandatory to tell the client tax information when sale confirmation is done.
    - **`EnableCancellationRequest`**: (``boolean``). Boolean `#!csharp true/false` that indicates whether the partner is allowed to request cancellations via API.
    - **`IsInsurancePolicyEnabled`**: (``boolean``). Boolean `#!csharp true/false` value that indicates whether the partner has [insurance policies](checkInsurancePolicies.md) available.
    - **`PaymentType`**: (``byte``). Indicates the payment type for the partner.

        ??? example "Possible values"
            - 1: Debit
            - 2: Credit
            - 3: Credit, except for groups
            - 4: Prepaid

--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/activity/catalogResponseExamples.md"
