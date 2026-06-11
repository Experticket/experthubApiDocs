# Perfiles de preguntas

Experticket permite asociar **preguntas** configurables a distintas entidades del proceso de venta. Las preguntas se agrupan en **perfiles de preguntas** (un perfil contiene una o más preguntas) y cada perfil se asocia a un **nivel** concreto: ticket, proveedor, venta, viaje o cliente.

Esta página explica los **tipos** de preguntas y el **flujo** de la API para consultarlas y responderlas. La documentación de cada endpoint implicado está enlazada a lo largo del texto.

!!! note "Preguntas de ticket"
    Las preguntas de **ticket** ya disponían de documentación previa y siguen un flujo ligeramente distinto al resto (se responden al [añadir el producto al carrito](../shoppingCart/add.md)). El resto de niveles —proveedor, venta, viaje y cliente— se documentan en esta página y se responden al [reservar](../shoppingCart/confirm.md) o [confirmar la venta](../shoppingCart/sale.md).

## Niveles de preguntas

Cada perfil de preguntas pertenece a uno de los siguientes niveles. La tabla indica de dónde se obtiene el identificador del perfil en el [catálogo](catalog.md) y dónde se envían las respuestas:

| Nivel | Descripción | Identificador de perfil en el catálogo | Dónde se responde |
| --- | --- | --- | --- |
| **Ticket** | Preguntas asociadas a un ticket concreto del producto (p. ej. nombre del asistente). | `Tickets[].TicketsQuestionsProfileId` | [Añadir al carrito](../shoppingCart/add.md) (por ticket) |
| **Proveedor** | Preguntas a nivel de proveedor, aplicables a la reserva de sus productos. Algunas solo se devuelven si se indica la sesión en los tickets. | `Providers[].ProviderQuestionsProfileIds` | [Reservar](../shoppingCart/confirm.md) / [Confirmar venta](../shoppingCart/sale.md) |
| **Venta** | Preguntas a nivel de venta, comunes a toda la transacción. | `SaleQuestionProfiles.SaleQuestionProfileIds` | [Reservar](../shoppingCart/confirm.md) / [Confirmar venta](../shoppingCart/sale.md) |
| **Viaje** | Preguntas relacionadas con la información de viaje de la venta. | `SaleQuestionProfiles.SaleTravelQuestionProfileIds` | [Reservar](../shoppingCart/confirm.md) / [Confirmar venta](../shoppingCart/sale.md) |
| **Cliente** | Preguntas asociadas al cliente comprador. | `SaleQuestionProfiles.ClientQuestionProfileIds` | [Reservar](../shoppingCart/confirm.md) / [Confirmar venta](../shoppingCart/sale.md) |

## Tipos de preguntas

Cada pregunta tiene un **tipo de dato** (`DataType`) que determina cómo se presenta y en qué propiedad debe enviarse su respuesta:

--8<-- "includes/enum/questionDataType.es.md"

Además, los perfiles y las preguntas se clasifican según dos criterios transversales:

### Estáticas o dinámicas

El perfil indica con la propiedad `AreDynamicQuestions` si sus preguntas son estáticas o dinámicas:

- **Estáticas** (`#!csharp AreDynamicQuestions = false`): las preguntas están definidas en la configuración del perfil y son fijas. Se obtienen siempre al [consultar perfiles de preguntas](CheckTicketsQuestions.md).
- **Dinámicas** (`#!csharp AreDynamicQuestions = true`): las preguntas se generan en **tiempo real** a partir de la integración del proveedor y pueden depender del producto y de la fecha de acceso. Para obtenerlas es **imprescindible** incluir en la consulta los productos con su fecha de acceso (campo `Products` de [consultar perfiles de preguntas](CheckTicketsQuestions.md)). Un mismo perfil puede combinar preguntas estáticas y dinámicas.

### Públicas o privadas

Las preguntas pueden definirse como **públicas** o **privadas**. Esta clasificación determina en qué taquillas se presentan al comprador:

- En las **taquillas públicas** (taquilla pública y su variante B2B pública) solo se muestran al comprador final las preguntas **públicas**.
- En los **canales profesionales** y al integrar a través de esta **API** se obtienen todas las preguntas aplicables al canal.

## Flujo en la API

El recorrido para trabajar con preguntas a través de la API es el siguiente:

1. **Catálogo.** Al obtener el [catálogo](catalog.md), cada entidad expone los identificadores de los perfiles de preguntas que tiene asociados (ver la tabla de [niveles](#niveles-de-preguntas)). Si una entidad no tiene perfil asociado, el campo correspondiente vendrá vacío y no será necesario tratar preguntas para ese nivel.
2. **Consultar perfiles de preguntas.** Con esos identificadores (y, para perfiles dinámicos, los productos con su fecha de acceso) se llama a [consultar perfiles de preguntas](CheckTicketsQuestions.md), que devuelve, por nivel, los perfiles con sus preguntas, tipos de dato, obligatoriedad, validaciones y valores predefinidos.
3. **Responder.**
    - Las preguntas de **ticket** se responden al [añadir el producto al carrito](../shoppingCart/add.md), dentro de cada ticket.
    - Las preguntas de **proveedor, venta, viaje y cliente** se responden en el campo `QuestionsProfiles` al [reservar](../shoppingCart/confirm.md) o al [confirmar la venta](../shoppingCart/sale.md).

## Flujo en las diferentes taquillas

Las preguntas se configuran una sola vez y se reutilizan en todos los canales de venta (taquillas), pero su presentación varía:

- **Taquilla pública / pública B2B**: el comprador final solo ve las preguntas **públicas** del canal. Las preguntas privadas no se le presentan.
- **Taquilla profesional / física**: el agente de venta ve todas las preguntas aplicables (públicas y privadas) configuradas para el canal.
- **Integración vía API (este flujo)**: el sistema integrador recibe todas las preguntas aplicables al consultar los perfiles y es responsable de presentarlas y de enviar sus respuestas en los pasos de reserva/confirmación.
