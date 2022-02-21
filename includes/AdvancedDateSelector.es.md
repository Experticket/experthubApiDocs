#### None

Los tickets **NO** pueden tener una fecha de acceso diferente a la de la transacción.

Por tanto, y siempre respecto al ticket, en Reserva de productos como en Creación de una transacción se prescindirá del valor AccessDateTime o se dejará a null.

#### DatePerTicketEnclosure

Los tickets SÍ pueden tener una fecha de acceso diferente a la de la transacción.

Como sabemos de Catálogo de productos, los tickets forman parte de un recinto (`TicketEnclosureId`). Pues bien, para el caso de `DatePerTicketEnclosure` cada recinto de ticket puede, opcionalmente, tener una fecha de acceso diferente.

Por ejemplo, imaginemos un producto llamado "Entrada Adulto Atracciones+Acuático", compuesto por dos tickets:

Ticket Adulto Atracciones. Correspondiente al recinto "Atracciones".
Ticket Adulto Acuático. Correspondiente al recinto "Acuático".
Para el caso de DatePerTicketEnclosure podremos hacer que el "Ticket Adulto Atracciones" tenga como fecha de entrada el 1 de abril y el "Ticket Adulto Acuático" tenga como fecha de entrada el 3 de mayo.

??? important "Limitación importante"
    Todos las fechas de acceso de todos los tickets que componen una transacción deben pertenecer al mismo conjunto de "PricesAndDates" (Catálogo de productos). Es decir, no podemos coger una fecha con un precio de 20€ y otra fecha con un precio de 25€.
