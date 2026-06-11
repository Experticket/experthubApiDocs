# Question profiles

Experticket lets you attach configurable **questions** to different entities of the sale process. Questions are grouped into **question profiles** (a profile contains one or more questions) and each profile is associated with a specific **level**: ticket, provider, sale, travel or client.

This page explains the **types** of questions and the **API flow** to query and answer them. The documentation for each endpoint involved is linked throughout the text.

!!! note "Ticket questions"
    **Ticket** questions were already documented and follow a slightly different flow from the rest (they are answered when [adding the product to the cart](../shoppingCart/add.md)). The remaining levels —provider, sale, travel and client— are documented on this page and are answered when [reserving](../shoppingCart/confirm.md) or [confirming the sale](../shoppingCart/sale.md).

## Question levels

Each question profile belongs to one of the following levels. The table shows where the profile identifier is obtained in the [catalog](catalog.md) and where the answers are sent:

| Level | Description | Profile identifier in the catalog | Where it is answered |
| --- | --- | --- | --- |
| **Ticket** | Questions associated with a specific product ticket (e.g. attendee name). | `Tickets[].TicketsQuestionsProfileId` | [Add to cart](../shoppingCart/add.md) (per ticket) |
| **Provider** | Provider-level questions, applicable to the reservation of its products. Some are only returned if the session is indicated in the tickets. | `Providers[].ProviderQuestionsProfileIds` | [Reserve](../shoppingCart/confirm.md) / [Confirm sale](../shoppingCart/sale.md) |
| **Sale** | Sale-level questions, common to the whole transaction. | `SaleQuestionProfiles.SaleQuestionProfileIds` | [Reserve](../shoppingCart/confirm.md) / [Confirm sale](../shoppingCart/sale.md) |
| **Travel** | Questions related to the travel information of the sale. | `SaleQuestionProfiles.SaleTravelQuestionProfileIds` | [Reserve](../shoppingCart/confirm.md) / [Confirm sale](../shoppingCart/sale.md) |
| **Client** | Questions associated with the buying client. | `SaleQuestionProfiles.ClientQuestionProfileIds` | [Reserve](../shoppingCart/confirm.md) / [Confirm sale](../shoppingCart/sale.md) |

## Question types

Each question has a **data type** (`DataType`) that determines how it is presented and which property its answer must be sent in:

--8<-- "includes/enum/questionDataType.en.md"

In addition, profiles and questions are classified according to two cross-cutting criteria:

### Static or dynamic

The profile indicates with the `AreDynamicQuestions` property whether its questions are static or dynamic:

- **Static** (`#!csharp AreDynamicQuestions = false`): the questions are defined in the profile configuration and are fixed. They are always returned when [checking question profiles](CheckTicketsQuestions.md).
- **Dynamic** (`#!csharp AreDynamicQuestions = true`): the questions are generated in **real time** from the provider's integration and may depend on the product and the access date. To retrieve them it is **mandatory** to include the products with their access date in the query (`Products` field of [checking question profiles](CheckTicketsQuestions.md)). A single profile can combine static and dynamic questions.

### Public or private

Questions can be defined as **public** or **private**. This classification determines in which sales channels they are presented to the buyer:

- In **public ticket shops** (public ticket shop and its public B2B variant) only **public** questions are shown to the end buyer.
- In **professional channels** and when integrating through this **API**, all questions applicable to the channel are returned.

## API flow

The path to work with questions through the API is as follows:

1. **Catalog.** When retrieving the [catalog](catalog.md), each entity exposes the identifiers of the question profiles attached to it (see the [levels](#question-levels) table). If an entity has no profile attached, the corresponding field will be empty and there is no need to handle questions for that level.
2. **Check question profiles.** With those identifiers (and, for dynamic profiles, the products with their access date), call [checking question profiles](CheckTicketsQuestions.md), which returns, per level, the profiles with their questions, data types, mandatory flags, validations and predefined values.
3. **Answer.**
    - **Ticket** questions are answered when [adding the product to the cart](../shoppingCart/add.md), within each ticket.
    - **Provider, sale, travel and client** questions are answered in the `QuestionsProfiles` field when [reserving](../shoppingCart/confirm.md) or [confirming the sale](../shoppingCart/sale.md).

## Flow across the different sales channels

Questions are configured once and reused across all sales channels (ticket shops), but their presentation varies:

- **Public / public B2B ticket shop**: the end buyer only sees the channel's **public** questions. Private questions are not presented to them.
- **Professional / physical ticket shop**: the sales agent sees all applicable questions (public and private) configured for the channel.
- **API integration (this flow)**: the integrating system receives all applicable questions when checking the profiles and is responsible for presenting them and sending their answers in the reserve/confirm steps.
