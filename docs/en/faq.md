# Frequently asked questions

## Activities

??? faq "Do I have to request the catalog with each sale I make?"
    No, the catalog must be processed once and only repeat this process in case its update date changes. We can see this by comparing the catalog date with the date returned by the endpoint [last catalog update date](docs/activity/lastCatalogUpdatedDate.md).

??? faq "When do I have to check the availability of a product or session?"
    We should only check the availability of those products that have the ``DaysWithLimitedCapacity`` field defined in the [catalog](docs/activity/catalog.md) or those [sessions](docs/activity/sessions.md) that have the ``AvailableCapacity`` field defined.

## Cart and sale

??? faq "Can I add products to the cart with quantity 0?"
    No, the system does not support adding products with quantity less than 1. It could cause an error that allows confirming the cart but not confirming the sale.

??? faq "Is it mandatory to indicate all the customer data when confirming the sale?"
    No. At a technical level, as specified in the [documentation](), only first and last names are required. It is possible that in the API certification process some clients require other data such as mail, identity document, etc.

    Keep in mind that those fields that you do not want to send must not be sent or sent as null, it is not possible to indicate the fields with an empty string, in this case the system interprets that they are defined and checks that the format of said data be correct.
