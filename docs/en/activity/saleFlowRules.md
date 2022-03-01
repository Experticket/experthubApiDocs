# Sales flow rules

The sales flow rules are used to automatically modify or add products to the sale according to a series of conditions that are met depending on the selected products.

??? info "Examples"
    - If four units of the product 'Product1' are added to the sale, a fifth unit of the product is automatically added at zero cost.
    - If the product 'Product2' is added and the product 'Product3' is also added, a 50% discount will be applied to the product 'Product3'.
    - For every 20 children added to a school group, a free teacher ticket is added.

!!! tip "Important"
    The rules are not cumulative for the same product. If a rule has already been applied to a product, it is discarded for subsequent rules. The order of application of the rules is marked by the ``Order`` field of the ``Rules`` node.

## Access method

**POST** activity/saleflowrules

## Response data structure

- **``Rules``**: array of rules.
    - **``Id``**: rule identifier.
    - **``Name``**: rule name.
    - **``Order``**: rule priority. This field indicates the order in which the rules will be applied, since more than one rule cannot be applied to the same product.
    - **``Inputs``**: array of products to which the rules apply.
        - **``ProductId``**: product identifier.
    - **``Processors``**: array of processors that is responsible for applying the conditions for the products of the ``Inputs`` field.
        - **``Value``**: number of products that must be added to the sale for this processor to be applied.
        - **``OutputIfExistsApplicability``**: value indicating how the outputs produced by this processor will be processed.

            ??? example "Possible values"
                - 0: undefined.
                - 1: first in order.
                - 2: the cheapest.
                - 3: the most expensive.
                - 4: all.

        - **``Outputs``**: are the outputs produced by the processor application.
            - **``ProductId``**: product identifier that produces this output.
            - **``Order``**: output priority. Applies if there are multiple outputs and the value of the ``OutputIfExistsApplicability`` field of the processor is equal to 1.
            - **``Quantity``**: number of products produced by this output.
            - **``ApplicationType``**: indicates if this output refers to a product that already existed in the purchase or a new one has been added.

                ??? example "Possible values"
                    - 1: a new product is added to the output.
                    - 2: update a product that already exists in ``Inputs``.

            - **``PriceModifierType``**: indicates which price modifier is applied to the product.

                ??? example "Possible values"
                    - 1: percent discount.
                    - 2: percent increase.
                    - 3: absolute value discount.
                    - 4: absolute value increase.
                    - 5: total price.

            - **``PriceModifierValue``**: indicates what price value applies to the product.

- **``Success``**: boolean (`#!csharp true/false`) that indicates if the request has been processed correctly.
- **``Timestamp``**: instant of time when the request is processed.
- **``ErrorMessage``**: in case of error includes a brief description of the problem.

### Response example

!!! info ""
    In the following example we can see two rules:

    - **Discount rule**: if the purchase contains the products "twy5yhbishk91" and "uspeg7nr5st96", the product "twy5yhbishk91" is updated with a €5 discount.
    - **Free product rule 3x2**: if the purchase contains the product "hwuk9huaqopwo" with quantity 2, the product "twy5yhbishk91" is added with a 100% discount.

--8<-- "includes/examples/activity/saleFlowRulesResponseExamples.md"
