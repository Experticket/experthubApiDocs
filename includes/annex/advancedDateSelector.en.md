**None**

The tickets **CANNOT** have an access date that differs from that of the sale.

Therefore, and always in reference to the ticket, when we add the product to the cart, the `AccessDateTime` from the ticket value will be ignored or it will be left null.

**DatePerTicketEnclosure**

The tickets CAN have an access date that differs from that of the sale.

As we know, according to Products catalog, As we know, according to Products catalog, the tickets form part of an enclosure (`TicketEnclosureId`). As such, for the DatePerTicketEnclosure each ticket enclosure can, optionally, have a different access date.

For instance, imagine a product called “Adult Ticket Amusement Park+Aquatic”, made up of two tickets:

- Adult Amusement Park Ticket. Corresponding to the enclosure "Amusement Park".
- Adult Aquatic Ticket. Corresponding to the enclosure “Aquatic”.

In the case of DatePerTicketEnclosure we can have the "Adult Amusement Park Ticket” with the entry date of April 1, and the "Adult Aquatic Ticket" with the entry date of May 3.

??? important "Important limitation"
    All access dates, of all tickets which compose one sale, should belong to the same set of `PricesAndDates`. In other words, we can pick a date with a price of €20, and another with a price of €25.
