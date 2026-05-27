# Check sales flow rules

Before making a purchase we can check if any of the rules that we have seen in [Sales Flow Rules](saleFlowRules.md) are going to be applied without having any consequences for practical purposes.

Once the query is launched, sufficient data will be returned, for information purposes, to know how the purchase would look if it was finished.

## Access method

**POST** activity/saleflowrules

## Request structure

- **``AccessDateTime``**: (``date``). Access date. *ISO 8601 format (yyyy-MM-dd)*.
- **``Products``**: (``list``). Products that make up the sale.
    - **``AccessDateTime``**: (``date``) ``Optional``. Access date. If defined at product level, it takes precedence over the date defined globally. *ISO 8601 format (yyyy-MM-dd)*.
    - **``ProductId``**: (``string``). Product identifier.
    - **``Quantity``**: (``int``) ``Optional``. Quantity. By default its value is 1.
- **``DynamicProviders``**: (``list``). Dynamic providers that make up the sale.
    - **``AccessDateTime``**: (``date``) ``Optional``. Access date. If defined at product level, it takes precedence over the date defined globally. *ISO 8601 format (yyyy-MM-dd)*.
    - **``ProviderId``**: (``string``). Dynamic provider identifier.
    - **``Quantity``**: (``int``) ``Optional``. Quantity. By default its value is 1.
- **`LanguageCode`**: (``string``) ``Optional``. Defines the language in which the texts will be displayed. By default, the language configured for the partner will be returned. *ISO 639-1 format*.

### Request example

!!! info "Example 1: free product rule (3x2)"
    In this example we are going to choose 4 products "hwuk9huaqopwo". Therefore, in the output data we should see the rule "Regla producto gratis 3x2" applied, seen in the [examples Sales flow rules](saleFlowRules.md#response-example). That is, since we order 4 "hwuk9huaqopwo" products, we must obtain two "twy5yhbishk91" products for free.
!!! info "Example 2: discount product rule and different access date (Discount)"
    In this example we are going to choose a product "twy5yhbishk91" and a product "uspeg7nr5st96" with a different access date. Therefore, in the output data we should see the "Regla Descuento" rule applied, seen in the [examples Sales flow rules](saleFlowRules.md#response-example). That is, we will see a €5 discount on the product "twy5yhbishk91".

--8<-- "includes/examples/activity/checkSaleFlowRulesQueryExamples.md"

## Response structure

- **``NotModifiedProducts``**: (``list``). Array containing products that have not been modified.
    - **``ProductId``**: (``string``). Product identifier.
    - **``AccessDateTime``**: (``date``). Product access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **``OriginalPrice``**: (``decimal``). Unchanged price of the product.
    - **``Price``**: (``decimal``). Final product price.
- **``ModifiedProducts``**: (``list``). Array containing modified products that were already included in the sale.
    - **``ProductId``**: (``string``). Product identifier.
    - **``AccessDateTime``**: (``date``). Product access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **``OriginalPrice``**: (``decimal``). Unchanged price of the product.
    - **``Price``**: (``decimal``). Final product price.
    - **``SaleFlowRuleId``**: (``string``). Rule identifier.
    - **``SaleFlowRuleCommercialName``**: (``string``). Descriptive name given to the rule so it can be displayed to the user.
    - **``SaleFlowRuleDescription``**: (``string``). Description of the applied rule.
    - **``SaleFlowRuleName``**: (``string``). Name of the applied rule.
- **``AddedProducts``**: (``list``). Array containing added products that were not included in the sale.
    - **``ProductId``**: (``string``). Product identifier.
    - **``AccessDateTime``**: (``date``). Product access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **``OriginalPrice``**: (``decimal``). Unchanged price of the product.
    - **``Price``**: (``decimal``). Final product price.
    - **``SaleFlowRuleId``**: (``string``). Rule identifier.
    - **``SaleFlowRuleCommercialName``**: (``string``). Descriptive name given to the rule so it can be displayed to the user.
    - **``SaleFlowRuleDescription``**: (``string``). Description of the applied rule.
    - **``SaleFlowRuleName``**: (``string``). Name of the applied rule.
--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/activity/checkSaleFlowRulesResponseExamples.md"
