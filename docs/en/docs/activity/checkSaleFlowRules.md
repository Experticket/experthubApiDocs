# Check sales flow rules

Before making a purchase we can check if any of the rules that we have seen in [Sales Flow Rules](saleFlowRules.md) are going to be applied without having any consequences for practical purposes.

Once the query is launched, sufficient data will be returned, for information purposes, to know how the purchase would look if it was finished.

## Access method

**POST** activity/saleflowrules

## Request data structure

- **``AccessDateTime``**: access date. *ISO 8601 format (yyyy-MM-dd)*.
- **``Products``**: products that make up the sale.
    - **``AccessDateTime``**: *optional*, access date. If defined, it has precedence over the date defined globally. *ISO 8601 format (yyyy-MM-dd)*.
    - **``ProductId``**: product identifier.
    - **``Quantity``**: *optional*, amount. By default its value is 1.

### Request example

!!! info "Example 1: free product rule (3x2)"
    In this example we are going to choose 4 products "hwuk9huaqopwo". Therefore, in the output data we should see the rule "Regla producto gratis 3x2" applied, seen in the [examples Sales flow rules](saleFlowRules.md#ejemplo-de-respuesta). That is, since we order 4 "hwuk9huaqopwo" products, we must obtain two "twy5yhbishk91" products for free.
!!! info "Example 2: discount product rule and different access date (Discount)"
    In this example we are going to choose a product "twy5yhbishk91" and a product "uspeg7nr5st96" with a different access date. Therefore, in the output data we should see the "Regla Descuento" rule applied, seen in the [examples Sales flow rules](saleFlowRules.md#response-example). That is, we will see a €5 discount on the product "twy5yhbishk91".

--8<-- "includes/examples/activity/checkSaleFlowRulesQueryExamples.md"

## Response data structure

- **``NotModifiedProducts``**: array containing products that have not been modified.
    - **``ProductId``**: product identifier.
    - **``AccessDateTime``**: product access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **``OriginalPrice``**: unchanged price of the product.
    - **``Price``**: final product price.
- **``ModifiedProducts``**: array containing modified products that were already included in the sale.
    - **``ProductId``**: product identifier.
    - **``AccessDateTime``**: product access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **``OriginalPrice``**: unchanged price of the product.
    - **``Price``**: final product price.
    - **``SaleFlowRuleId``**: rule identifier.
    - **``SaleFlowRuleCommercialName``**: descriptive name given to the rule to display to the user.
    - **``SaleFlowRuleDescripción``**: description of the applied rule.
    - **``SaleFlowRuleName``**: applied rule name.
- **``AddedProducts``**: array containing added products that were not included in the sale.
    - **``ProductId``**: product identifier.
    - **``AccessDateTime``**: product access date. *ISO 8601 format (yyyy-MM-dd)*.
    - **``OriginalPrice``**: unchanged price of the product.
    - **``Price``**: final product price.
    - **``SaleFlowRuleId``**: rule identifier.
    - **``SaleFlowRuleCommercialName``**: descriptive name given to the rule to display to the user.
    - **``SaleFlowRuleDescripción``**: description of the applied rule.
    - **``SaleFlowRuleName``**: applied rule name.
--8<-- "includes/responseBaseDocumentation.en.md"

### Response example

--8<-- "includes/examples/activity/checkSaleFlowRulesResponseExamples.md"
