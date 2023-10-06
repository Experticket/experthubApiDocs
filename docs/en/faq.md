# Frequently Asked Questions

## Activities

??? faq "Do I have to consult the catalog with every sale I make?"
    No, the catalog should be processed once and only repeat this process if its update date changes. We can do this by comparing the catalog date with the date returned by the [last catalog update date endpoint](docs/activity/lastCatalogUpdatedDate.md).

??? faq "When do I need to check the availability of a product or session?"
    You only need to check the availability of products that have the ``DaysWithLimitedCapacity`` field defined in the [catalog](docs/activity/catalog.md), or those [sessions](docs/activity/sessions.md) that have the AvailableCapacity field defined.

## Cart and Sale

??? faq "Can I add products to the cart with a quantity of 0?"
    No, the system does not allow adding products with a quantity less than 1. Doing so could cause an error that allows confirming the cart but not confirming the sale.

??? faq "Is it mandatory to provide all customer data when confirming the sale?"
    No. From a technical perspective, as specified in the [documentation](), only the first name and last name are mandatory. During the API certification process, some clients may require additional data such as email, ID card number (DNI), etc.

    It's important to note that any fields that are not desired to be sent should not be included in the request or should be sent as null. It is not possible to indicate fields with an empty string, as the system interprets them as defined fields and checks that the data format is correct.
