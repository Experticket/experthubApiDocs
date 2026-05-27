# Quote refund insurance policies

Using this method, we can check the refund insurance policies available for one or more products and one or more access dates.

!!! success ""
    If **`IsInsurancePolicyEnabled`** is not defined as `#!csharp true` in the [catalog](catalog.md) `PartnerSettings`, or if the provider/category/product does **NOT** have the **`IsInsurable`** field from the [catalog](catalog.md) defined as `#!csharp true`, then this call is not necessary.

!!! warning ""
    If the provider/category/product has the **`IsInsurable`** field from the [catalog](catalog.md) defined as `#!csharp true`, then this call must be made every time you want to offer the customer the option of purchasing a refund insurance policy for 1 or N products.

!!! info "Why are we talking about refund insurance policy?"

    When finishing a sale, there is a possibility of purchasing a refund insurance policy for one or more of the products included in the sale.

## Access method

**POST** /activity/InsurancePolicyCheck

## Request structure

- **`LanguageCode`**: (``string``). Defines the language in which the texts will be displayed. *ISO 639-1 format*.
- **`Sale`**: (``object``). Sale data. It is important to note that **ALL** items included in the sale must be sent (not only the insurable products), except for those added by [sale flow rules](checkSaleFlowRules.md).
    - **`Products`**: (``list``). Array with all the products included in the sale. Combined products must not be included here.
        - **`Id`**: (``string``). Unique identifier used as an echo identifier, meaning it will be returned in the response data.
        - **`ProductId`**: (``string``). Product identifier.
        - **`AccessDate`**: (``date``). Access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **`CombinedProducts`**: (``list``). Array of combined products.
        - **`Id`**: (``string``). Unique identifier used as an echo identifier, meaning it will be returned in the response data.
        - **`CombinedProductId`**: (``string``). Combined product identifier.
        - **`Products`**: (``list``). Array of products included in the combined product, with the same structure as the product list used in the sale.
    - **`Packages`**: (``list``). Array of packages.
        - **`EchoToken`**: (``string``). Token that identifies the request sequence. See [extended catalog](../package/fullCatalog.md#response-structure).
        - **`PackageId`**: (``string``). Package identifier.
        - **`Activities`**: (``list``). Activities included in the package.
            - **`Id`**: (``string``). Unique identifier used as an echo identifier, meaning it will be returned in the response data.
            - **`ProductId`**: (``string``). Product identifier.
            - **`AccessDate`**: (``date``). Access date. ISO 8601 format (yyyy-MM-dd).
    - **`Accommodations`**: (``list``). Array of accommodations.
        - **`EchoToken`**: (``string``). Token that identifies the request sequence. See [extended catalog](../package/fullCatalog.md#response-structure).
        - **`RateId`**: (``string``). Rate identifier.
- **`DiscountCouponCodes`**: (``object``). Array of discount coupon codes included in the sale. This information is necessary in order to calculate the final price of the policy to be quoted.

### Request examples

--8<-- "includes/examples/activity/checkInsurancePoliciesQueryExamples.md"

## Response structure

- **`InsurancePolicies`**: (``list``). Array of refund insurance policies.
    - **`Id`**: (``string``). Policy identifier.
    - **`Name`**: (``string``). Policy name.
    - **`Quote`**: (``decimal``). Policy quote amount, i.e. the price charged to the customer for the policy.
    - **`CoverageAmount`**: (``decimal``). Coverage amount of the policy.
    - **`Sale`**: (``object``). Sale information.
        - **`Products`**: (``list``). Array of included products.
            - **`Id`**: (``string``). Echo identifier returned in the response.
            - **`ProductId`**: (``string``). Product identifier.
            - **`AccessDate`**: (``date``). Access date. *ISO 8601 format (yyyy-MM-dd)*.
            - **`Price`**: (``decimal``). Product price for that date.
            - **`CoverageAmount`**: (``decimal``). Amount covered by the refund insurance.
            - **`IsCovered`**: (``boolean``). Indicates whether it is covered by the refund insurance.
    --8<-- "includes/responseBaseDocumentation.en.md"

### Response examples

--8<-- "includes/examples/activity/checkInsurancePoliciesResponseExamples.md"
