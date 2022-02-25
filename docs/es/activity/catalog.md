# Catálogo de actividades

El primer paso será obtener todo el catálogo completo de proveedores, categorías (productBases) y productos para su tratamiento interno.

La información del catálogo incluye los identificadores únicos de Proveedor, Producto y Ticket que posteriormente se usarán para añadir cualquier producto al carrito.

También incluirá otros datos como el precio de los productos dependiendo de las fechas, o las condiciones comerciales del producto.

Siguiendo con nuestro ejemplo, podría darse el caso en el que el producto "Entrada 2x1 Niño" del proveedor PAC baje el precio y aumente el periodo de validez de la venta.

## Método de acceso

**POST** /activity/catalog

## Estructura de datos de envío

Para obtener el catálogo podemos utilizar diferentes filtros en el cuerpo del método. Aunque podemos realizar la llamada sin ningún filtro.

Cada filtro se considerará un ***AND***. Por ejemplo, pueden filtrarse por varios *ProductIds* pero no tiene sentido filtrar por *ProviderIds* y por *ProductIds* siendo este último de un proveedor diferente al del primer filtro.

- **`ProviderIds`**: lista identificadores de proveedor.
- **`ProductBaseIds`**: lista identificadores de categoría.
- **`ProductIds`**: lista identificadores de producto.
- **`FromDate`**: fecha de inicio. No permite valores menores al día actual. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`ToDate`**: fecha de fin. Por defecto su valor es el de la fecha correspondiente a dentro de un año. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`ReferenceDate`**: exige que el día que se tome como referencia para el cálculo de precios y disponibilidades no sea hoy, sino el indicado. Por ejemplo se usará si los precios cambian dependiendo de los días que quedan hasta la fecha de la entrada. *Formato ISO 8601 (yyyy-MM-dd)*
- **`LanguageCode`**: define el idioma en que se mostrarán los textos del catálogo (nombre, descripción, condiciones de proveedor, producto, etc.). Por defecto se devolverá el idioma configurado para el colaborador. *Formato ISO 639-1*.
- **`ShowProductsOutOfActiveDateRange`**: si su valor es `#!csharp true`, la respuesta devolverá productos en los que el día de hoy (o el día indicado en `ReferenceDate`) está fuera de su rango de fechas de venta. Por ejemplo, si estamos en diciembre y hay productos que se pueden vender a partir de enero, poniendo este valor a true nos permitirá descubrir que existen esos productos.

### Ejemplos de llamadas

--8<-- "includes/examples/activity/catalogQueryExamples.md"

## Estructura de datos de respuesta

- **`LastUpdatedDateTime`**: fecha de la última modificación del catálogo.
- **`Providers`**: array de proveedores.
    - **`ProviderId`**: identificador del proveedor. Alfanumérico de 13 caracteres.
    - **`ProviderName`**: nombre del proveedor.
    - **`ProviderDescription`**: descripciones del proveedor.
    - **`ProviderCommercialConditions`**: condiciones comerciales de proveedor. Si no existen, este campo no se mostrará.
    - **`ProviderAccessConditions`**: condiciones de acceso del proveedor. Si no existen, este campo no se mostrará.
    - **`AdvancedDateSelectorMethodName`**: nombre del método que define si los tickets de un producto pueden tener su propia fecha de acceso particular.

        ??? example "Posibles valores"
            --8<-- "includes/annex/advancedDateSelector.es.md"

    - **`CancellationPolicy`**: indica las políticas de cancelación que se aplican al cancelar una venta de este proveedor. Si un producto concreto no tiene políticas de cancelación se aplicarán estas.
        - **`IsRefundable`**: indica si el cliente puede cancelar gratis en algún momento.
        - **`Rules`**: reglas que se aplican al efectuar la cancelación.
            - **`HoursInAdvanceOfAccess`**: indica la cantidad de horas de antelación con respecto a la fecha de acceso a partir de las cuales se aplicará la penalización de precio indicada en `Percentage`.
            - **`Percentage`**: porcentaje de penalización sobre el precio de la entrada.
    - **`DemandAccessDate`**: indica si la fecha de acceso es necesaria. En caso de no ser necesaria, al añadir el producto al carrito debe usarse la fecha de compra.
    - **`TaxType`**: indica el tipo de impuesto de los productos del proveedor.

        ??? example "Posibles valores"
            - 0: IVA
            - 1: IGIC

    - **`Type`**: indica el tipo de proveedor. Por defecto será 0.

        ??? example "Posibles valores"
            - 0: Actividad
            - 1: Alojamiento
            - 2: Transporte

    - **`IsForGroups`**: indica si los productos del proveedor están destinados a la venta para grupos.
    - **`LimitOfNumberOfPeopleToBeGroup`**: límite del número de personas que conforman un producto a partir del cual la venta se considera para "grupos". Por ejemplo, si este límite es "19" y el proveedor no es para grupos (`#!csharp IsForGroups == false`), no se aceptarán ventas con 20 o más personas. Por contra, si el proveedor es para grupos (`#!csharp IsForGroups == true`), solo se aceptarán ventas para 20 o más personas.
    - **`Logo`**: url para descargar la imagen del logotipo del proveedor.
    - **`Location`**: información de localización.
        - **`CountryCode`**: código de país (es, fr...).
        - **`City`**: ciudad.
        - **`Address`**: dirección.
        - **`ZipCode`**: código postal.
        - **`Lat`**: latitud.
        - **`Lng`**: longitud.
    - **`Ticket enclosures`**: información de los recintos del proveedor.
        - **`TicketEnclosureId`**: identificador del recinto.
        - **`TicketEnclosureName`**: nombre del recinto.
        - **`TicketEnclosureConditions`**: *opcional*, condiciones del recinto.
        - **`TypeOfPersonDefinitionTypeChild`**: *opcional*, indica qué atributo se aplica a la persona para considerarla niño.

            ??? example "Posibles valores"
                --8<-- "includes/annex/typeOfPersonDefinition.es.md"

        - **`TypeOfPersonDefinitionValueChild`**: *opcional*, indica el valor asignado al tipo de persona niño.
        - **`TypeOfPersonDefinitionTypeAdult`**: *opcional*, indica qué atributo se aplica a la persona para considerarla adulto.

            ??? example "Posibles valores"
                --8<-- "includes/annex/typeOfPersonDefinition.es.md"

        - **`TypeOfPersonDefinitionValueAdult`**: *opcional*, indica el valor asignado al tipo de persona adulto.
        - **`TypeOfPersonDefinitionTypeSenior`**: *opcional*, indica qué atributo se aplica a la persona para considerarla senior.

            ??? example "Posibles valores"
                --8<-- "includes/annex/typeOfPersonDefinition.es.md"

        - **`TypeOfPersonDefinitionValueSenior`**: *opcional*, indica el valor asignado al tipo de persona senior.
        - **`Sessions`**: *opcional*, define la relación entre sesiones y contenido. Antes de continuar, es imprescindible estudiar el apartado [obtención de sesiones](sessions.md).
            - **`SessionContentProfileId`**: para más información acerca de este identificador, consulte la página de [sesiones](sessions.md).
            - **`SessionGroupProfileId`**: para más información acerca de este identificador, consulte la página de [sesiones](sessions.md).
            - **`SessionsGroupSessionContents`**: define la relación entre grupos de sesión y contenidos de sesión. Es decir, todas las sesiones del grupo de sesión tendrán asignado el contenido de sesión. `SessionsGroupSessionContents` es excluyente respecto a `SessionSessionContents`.
                - **`SessionsGroupId`**: identificador del grupo de sesiones.
                - **`SessionContentId`**: identificador de contenido de sesión.
            - **`SessionSessionContents`**: define la relación entre sesiones y contenidos de sesión. `SessionSessionContents` es excluyente respecto a `SessionsGroupSessionContents`.
                - **`SessionId`**: identificador de sesión.
                - **`SessionContentId`**: identificador de contenido de sesión.
                - **`SessionTime`**: fecha y hora de la sesión.
                - **`HasLimitedCapacity`**: indica si la sesión tiene aforo. De ser así será imprescindible consultar la disponibilidad de la sesión antes de crear una venta. Más información al respecto en [obtención de aforo disponible](availability.md).
            - **`TicketEnclosureAutoAssignSessionType`**: indica qué atributo se aplica a la hora de elegir sesiones. Pueden ser sesiones auto asignadas por el sistema, elegibles, o una mezcla de los dos casos. En el caso de sesiones auto asignadas se puede comprobar qué sesiones se van a asignar antes de añadir el producto al carrito mediante el [método para comprobar la sesión autoasignada](autoAssignSession.md).

                ??? example "Posibles valores"
                    - **0: No**. Las sesiones no se auto asignarán. Deben definirse durante el flujo de venta.
                    - **1: IfNotSet**. Las sesiones se autoasignarán, siempre y cuando no se haya definido durante el flujo de venta.
                    - **2: ForceSet**. Las sesiones se autoasignarán siempre de forma forzada, ignorando si se han definido durante el flujo de venta.

        - **`ProductBases`**: array de categorías.
            - **`ProductBaseId`**: identificador de la categoría. Alfanumérico de 13 caracteres.
            - **`ProductBaseName`**: nombre de la categoría.
            - **`ProductBaseDescription`**:  descripción de la categoría. Suele contener las condiciones comunes al todos sus productos.
            - **`DaysWithLimitedCapacity`**: fechas en los que todos los productos de esta categoría tienen un aforo limitado. Por tanto, será imprescindible consultar la disponibilidad de la categoría antes de crear una venta. Las fechas tendrán *formato ISO 8601 (yyyy-MM-dd)*, y estarán separadas entre sí por una coma. Más información al respecto en el punto [obtención de aforo disponible](availability.md).
            - **`LimitOfNumberOfPeopleToBeGroup`**: *opcional*, mismo significado que la propiedad `LimitOfNumberOfPeopleToBeGroup` en el nodo `Provider`. Si está especificado se usará el más restrictivo entre este valor y el de proveedor.
            - **`Products`**: array de productos.
                - **`ProductId`**: identificador del producto. Alfanumérico de 13 caracteres.
                - **`ProductName`**: nombre del producto.
                - **`SuggestedSalesProductName`**: nombre sugerido del producto de cara a la venta.
                - **`ProductDescription`**: descripción del producto. Suele contener las condiciones del producto.
                - **`ProductInternalConsiderations`**: consideraciones internas del producto que solo debe conocer el colaborador.

                    ???+ danger "Importante"
                        **NUNCA** mostrar al cliente final.

                - **`ProductCancellationConditions`**: condiciones de cancelación para el producto.
                - **`CancellationPolicy`**: indica las políticas de cancelación que se aplican al cancelar una venta de este producto. Si este nodo está presente, tiene preferencia sobre el nodo `CancellationPolicy` del proveedor.
                    - **`IsRefundable`**: indica si el cliente puede cancelar gratis en algún momento.
                    - **`Rules`**: reglas que se aplican al efectuar la cancelación.
                        - **`HoursInAdvanceOfAccess`**: indica la cantidad de horas de antelación con respecto a la fecha de acceso a partir de las cuales se aplicará la penalización de precio indicada en `Percentage`.
                        - **`Percentage`**: porcentaje de penalización sobre el precio de la entrada.
                - **`StartIsActiveDate`**: *opcional*, si existe, define la fecha a partir de la cual es posible vender el producto.
                - **`EndIsActiveDate`**: *opcional*, si existe, define la fecha hasta la cual es posible vender el producto.
                - **`DaysWithLimitedCapacity`**: fechas en los que el producto tiene un aforo limitado. Por tanto, será imprescindible consultar la disponibilidad del producto antes de crear una venta. Las fechas tendrán *formato ISO 8601 (yyyy-MM-dd)*, y estarán separadas entre sí por una coma. Más información al respecto en el punto [obtención de aforo disponible](availability.md).
                - **`HoursInAdvanceOfPurchase`**: horas de antelación de la compra respecto a las 00:00 del día siguiente al de la visita. Por ejemplo, si un producto tiene `HoursInAdvanceOfPurchase = 4`, y un cliente realiza una compra para el 15 de Agosto, el límite de tiempo que tiene el producto para venderse son las 20:00 del propio 15 de Agosto (es decir, 4 horas antes de las 00:00 del 16 de Agosto). Esto es importante, por ejemplo, para que un cliente no compre los productos para un día cuando el recinto ya está a cerrado.
                - **`MaxHoursInAdvanceOfPurchase`**: *opcional*, horas máximas de antelación de la compra respecto a las 00:00 del día siguiente al de la visita. Por ejemplo, si un producto tiene `MaxHoursInAdvanceOfPurchase = 240`, y un cliente realiza una compra para el 15 de Agosto, el producto no puede venderse antes del 6 de Agosto (es decir, 240 horas = 10 días antes de las 00:00 del 16 de Agosto). Esto es útil, por ejemplo, para limitar el período de venta de un producto a un plazo de días previos.
                - **`MinimumNumberByTransaction`**: cantidad mínima de productos por cada venta. Por defecto es 1. Por ejemplo, imaginemos un producto del tipo "Entrada con descuento a partir de 3 productos". En ese caso MinimumNumberByTransaction sería 3.
                - **`NumberOfPeople`**: número de personas que computan para considerar una venta como "grupo". Es decir, computa para el límite `LimitOfNumberOfPeopleToBeGroup`.
                - **`NumberOfAdults`**: número de adultos, incluidos en el campo `NumberOfPeople`.
                - **`NumberOfBabies`**: número de bebés, incluidos en el campo `NumberOfPeople`.
                - **`NumberOfChildren`**: número de niños, incluidos en el campo `NumberOfPeople`.
                - **`NumberOfSenior`**: número de seniors, incluidos en el campo `NumberOfPeople`.
                - **`NumberOfGeneric`**: número de genéricos, incluidos en el campo `NumberOfPeople`. Es un campo muy útil, por ejemplo, si un producto vale tanto para adulto como para niño como para senior.
                - **`RequiresRealTimePrice`**: indica si el producto requiere precio en tiempo real.

                    ??? tip "Implicaciones"
                        En caso de estar definido como `#!csharp true` será necesario antes de iniciar cualquier venta hacer la llamada para [consultar el precio en tiempo real](realTimePrices.md). Ya que el precio del producto puede ser diferente en función de algunos criterios.

                - **`ValidDays`**: días de validez.
                - **`ValidDaysType`**: tipo de días válidos.

                    ??? example "Posibles valores"
                        - 0: consecutivos.
                        - 1: no consecutivos.

                - **`PriceMode`**: indica el tipo de precio.

                    ??? example "Posibles valores"
                        - 1: PVP.
                        - 2: precio neto.

                - **`Commission`**: en caso de que `PriceMode = PVP`, nos indica la comisión.
                    - **`Type`**: indica el tipo de comisión aplicada.

                        ??? example "Posibles valores"
                            - 1: porcentaje.
                            - 2: valor absoluto.

                    - **`Value`**: valor de esa comisión.

                        ??? info "Ejemplo"
                            - si `Type = 1` y `Value = 10`, indica que la comisión es del 10% respecto al `Price` del producto. Es decir, si el `Price` es igual a 100€, la comisión calculada sería de 10€.
                            - si `Type = 2` y `Value = 3`, indica que la comisión por producto es de 3€.

                - **`AccessDateCriteria`**: indica el criterio para la fecha de acceso.

                    ??? example "Posibles valores"
                        --8<-- "includes/annex/accessDateCriteria.es.md"

                - **`BarcodeAssignment`**: *opcional*, indica a qué se va asignar el código de barras.

                    ??? example "Posibles valores"
                        - 1: Ticket (valor por defecto si `BarcodeAssignment` no viene definido).
                        - 2: Persona.

                        ???+ info "Ejemplo"
                            El producto "Entrada dos días" compuesto por un adulto y 2 tickets (entrada día 1, entrada día 2):

                            - `BarcodeAssignment = Ticket`: cada uno de los tickets tendrá su propio código de barras.
                            - `BarcodeAssignment = Persona`: solo habrá un código de barras (compartido por ambos tickets). Una consecuencia directa de este caso la tendríamos a la hora de imprimir un PDF con las entradas, ya que solo tendríamos que imprimir un PDF del producto, dado que a pesar de tener dos tickets solo hay un código de barras.

                - **`PricesAndDates`**: array de "*precio y fechas*". Tiene una doble funcionalidad. Por una parte nos define qué fechas de acceso tiene disponible el producto, y por otra parte nos define qué precio se aplica a qué fechas.
                    - **`Price`**: precio.
                    - **`Currency`**: moneda.
                    - **`CurrencyName`**: nombre de la moneda.
                    - **`Dates`**: las fechas tendrán *formato ISO 8601 (yyyy-MM-dd)* y estarán separadas entre sí por una coma.
                    - **`OriginalPrice`**: *opcional*, precio del producto antes de aplicar descuentos si existen.
                    - **`TaxBreakdown`**: array con el desglose de impuestos.
                        - **`TaxPercentage`**: porcentaje de impuesto (sobre 100).
                        - **`PriceWithoutTaxes`**: precio sin impuestos.
                        - **`PriceWithTaxes`**: precio con impuestos.
                - **`Release`**: *opcional*, número de días de antelación necesarios para que el cliente pueda cancelar el producto sin coste.

                    ??? info "Ejemplo"
                        - 0: El cliente puede cancelar el día de entrada al parque sin coste.
                        - 1: El cliente puede cancelar un día antes de la entrada al parque sin coste.

                - **`SalesDocumentSettings`**: configuraciones respecto al documento de acceso (pdf, passbook). Esta información también vendrá como resultado al confirmar una venta.

                    ??? tip "Consejo"
                        Si se utilizan los documentos generados por nosotros no será necesario tener en cuenta estas configuraciones. De lo contrario, debéis tenerlas en consideración.

                    - **`Disable`**: indica si no se generará documento de acceso para este producto.
                    - **`ShowPrice`**: indica si se debe mostrar el precio en el documento de acceso.
                    - **`AccessDateCriteriaOpenDateSalesDocument`**: solo en el caso de que `AccessDateCriteria == 1` (fecha abierta). Indica qué debemos informar al cliente respecto a la fecha de acceso.

                        ??? example "Posibles valores de AccessDateCriteria y AccessDateCriteriaOpenDateSalesDocument"
                            --8<-- "includes/annex/accessDateCriteria.es.md"

                - **`Tickets`**: *opcional*, array de tickets. En caso de que el producto no trabaje con tickets, este campo no existirá.
                    - **`TicketId`**: identificador de ticket. Alfanumérico de 13 caracteres.
                    - **`IsQuotaTicket`**: booleano que indica si el ticket es o no de tipo aforo, lo que quiere decir que en caso de ser `#!csharp true` el ticket computará para el total de aforo necesario para reservar el producto. Por ejemplo, si tenemos un producto donde tiene 3 tickets definidos pero únicamente 2 de ellos son de tipo aforo, entonces al consultar la disponibilidad para esté producto hay que tener en cuenta que a nivel de aforo necesita 2 de disponibilidad. En otras palabras en caso de que el aforo disponible fuese 1 no podríamos reservar este producto. Para más información consulta el endpoint [obtención de aforo disponible](availability.md).
                    - **`TicketName`**: nombre del ticket.
                    - **`TicketConditions`**: *opcional*, condiciones del ticket.
                    - **`TicketEnclosureId`**: identificador del recinto al que pertenece el ticket. Varios tickets puede pertenecer al mismo recinto.
                    - **`FromAccessDay`** y **`ToAccessDay`**: si están definidos, indican para qué días respecto a la primera fecha de acceso es válido el ticket.

                        ???+ tip "Consejo"
                            El resultado de la llamada para confirmar una venta ya nos devuelve el rango de fechas de acceso de cada ticket. Por tanto es totalmente factible no tratar `FromAccessDay` y `ToAccessDay` y basarnos en lo que nos devuelva dicha llamada.

                        ??? info "Ejemplo"

                            - Si el ticket define FromAccessDay = 1 y ToAccessDate = 1, el cliente deberá usarlo el primer día de acceso.
                            - Si el ticket define FromAccessDay = 2 y ToAccessDate = 2, el cliente deberá usarlo el segundo día de acceso.
                            - Si el ticket define FromAccessDay = 1 y ToAccessDate = 2, el cliente podrá entrar o el primer o el segundo día.
                            - Si el ticket define FromAccessDay = 2 y ToAccessDate no definido, el cliente podrá entrar desde el segundo día hasta un día indefinido, por ejemplo hasta que termine la temporada, *salvo que las condiciones del producto indiquen lo contrario*.
                            - Si el ticket no define ni FromAccessDay ni ToAccessDate, el cliente solo podrá entrar el primer día, *salvo que se indique lo contrario en las condiciones*.

                    - **`TypeOfPerson`**: *opcional*, define el tipo de persona y su numeración.
                        - **`Type`**: indica el tipo de persona.

                            ??? example "Posibles valores"
                                - 1: Bebé
                                - 2: Niño
                                - 3: Adulto
                                - 4: Senior
                                - 5: Genérico

                        - **`PersonNumber`**: identificador del número de persona por tipo.

                        ??? example "Ejemplo"
                            - Producto "Entrada 3x2" compuesto por dos adultos y un niño y definido por tres tickets:
                                - Ticket Adulto: adulto 1 (Type = 3, PersonNumber = 1)
                                - Ticket Adulto: adulto 2 (Type = 3, PersonNumber = 2)
                                - Ticket Niño: niño 1 (Type = 2, PersonNumber = 1)
                            - Producto "Entrada 2x1 más segundo día consecutivo" compuesto por dos adultos y 4 tickets:
                                - Ticket Adulto primer día: adulto 1 (Type = 3, PersonNumber = 1)
                                - Ticket Adulto primer día: adulto 2 (Type = 3, PersonNumber = 2)
                                - Ticket Adulto segundo día: adulto 1 (Type = 3, PersonNumber = 1)
                                - Ticket Adulto segundo día: adulto 2 (Type = 3, PersonNumber = 2)

                - **`ProductPaxGroupingId`**: *opcional*, identificador de la agrupación de productos a la que pertenece el producto.

        - **`ProductPaxGroupings`**: agrupaciones de productos cuya diferencia principal son las personas que lo componen.
            - **`ProductPaxGroupingId`**: identificador de la agrupación. Alfanumérico de 13 caracteres.
            - **`ProductPaxGroupingName`**: nombre de la a agrupación.

    - **`Urls`**: *opcional*, array de urls para acceder a la página de la taquilla del proveedor. Sólo en el caso de tener DNS personalizadas.
        - **`LanguageCode`**: código del idioma con el que se va a acceder. Representado mediante el *formato ISO 639-1*.
        - **`Url`**: url de acceso.

- **`CombinedProducts`**: array de productos combinados.
    - **`CombinedProductId`**: identificador de producto combinado.
    - **`Name`**: nombre del producto combinado.
    - **`PriceFrom`**: precio "*desde*" para el producto combinado.
    - **`PriceTo`**: precio "*hasta*" para el producto combinado.
    - **`Products`**: array de productos que forman parte del producto combinado.
        - **`ProductId`**: identificador del producto.
    - **`RequiresRealTimePrice`**: indica si requiere consultar el precio en tiempo real para el producto combinado. Véase [obtención del precio en tiempo real](realTimePrices.md)
- **`PartnerSettings`**: indica las configuraciones del colaborador.
    - **`DemandClientData`**: valor de verdad `#!csharp true/false` que indica si es obligatorio indicar datos del cliente al confirmar una venta.
    - **`EnableCancellationRequest`**: valor de verdad `#!csharp true/false` que indica si el colaborador tiene permitido solicitar cancelaciones vía API.
    - **`PaymentType`**: indica el tipo de pago que realiza el colaborador.

        ??? example "Posibles valores"
            - 1: Débito
            - 2: Crédito
            - 3: Crédito excepto para grupos
            - 4: Prepago

- **`Success`**: valor de verdad, `#!csharp true/false` que indica si la obtención del catálogo ha sido o no correcta.
- **`Timestamp`**: momento de la obtención del catálogo.
- **`ErrorMessage`**: mensaje de error explicando por qué la obtención del catálogo no ha sido correcta. En caso que haya sido correcta, devolverá `#!csharp null`.

### Ejemplo de respuesta

--8<-- "includes/examples/activity/catalogResponseExamples.md"
