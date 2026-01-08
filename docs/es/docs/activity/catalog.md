# Catálogo de actividades

El primer paso será obtener todo el catálogo completo de proveedores, categorías (productBases) y productos para su tratamiento interno.

La información del catálogo incluye los identificadores únicos de Proveedor, Producto y Ticket que posteriormente se usarán para añadir cualquier producto al carrito.

También incluirá otros datos como el precio de los productos dependiendo de las fechas, o las condiciones comerciales del producto.

!!! caution "Mal uso del API"
    Un mal uso de esta llamada sería realizar una consulta con cada venta que se inicia, el uso correcto debe ser almacenar y procesar de forma local y consultar periódicamente la [fecha de la última modificación del catálogo](lastCatalogUpdatedDate.md). Únicamente en caso de que esa fecha de modificación sea posterior a la obtenida en el catálogo debemos volver a obtener el catálogo.

## Método de acceso

**POST** /activity/catalog

## Estructura de la petición

Para obtener el catálogo podemos utilizar diferentes filtros en el cuerpo del método. Aunque podemos realizar la llamada sin ningún filtro.

Cada filtro se considerará un ***AND***. Por ejemplo, pueden filtrarse por varios *ProductIds* pero no tiene sentido filtrar por *ProviderIds* y por *ProductIds* siendo este último de un proveedor diferente al del primer filtro.

- **`ProviderIds`**: (``list``) ``Opcional``. Lista identificadores de proveedor.
    - **``(string)``**: ``Opcional``. Identificador del proveedor.
- **`ProductBaseIds`**: (``list``) ``Opcional``. Lista identificadores de categoría.
    - **``(string)``**: ``Opcional``. Identificador del ProductBase.
- **`ProductIds`**: (``list``) ``Opcional``. Lista identificadores de producto.
    - **``(string)``**: ``Opcional``. Identificador de producto.
- **`FromDate`**: (``date``) ``Opcional``. Fecha de inicio. No permite valores menores al día actual. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`ToDate`**: (``date``) ``Opcional``. Fecha de fin. Por defecto su valor es el de la fecha correspondiente a dentro de un año. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`ReferenceDate`**: (``date``) ``Opcional``. Exige que el día que se tome como referencia para el cálculo de precios y disponibilidades no sea hoy, sino el indicado. Por ejemplo se usará si los precios cambian dependiendo de los días que quedan hasta la fecha de la entrada. *Formato ISO 8601 (yyyy-MM-dd)*
- **`LanguageCode`**: (``string``) ``Opcional``. Define el idioma en que se mostrarán los textos del catálogo (nombre, descripción, condiciones de proveedor, producto, etc.). Por defecto se devolverá el idioma configurado para el colaborador. *Formato ISO 639-1*.
- **`ShowProductsOutOfActiveDateRange`**: (``boolean``) ``Opcional``. Si su valor es `#!csharp true`, la respuesta devolverá productos en los que el día de hoy (o el día indicado en `ReferenceDate`) está fuera de su rango de fechas de venta. Por ejemplo, si estamos en diciembre y hay productos que se pueden vender a partir de enero, poniendo este valor a true nos permitirá descubrir que existen esos productos.

### Ejemplos de llamadas

--8<-- "includes/examples/activity/catalogQueryExamples.md"

## Estructura de la respuesta

- **`LastUpdatedDateTime`**: (``dateTime``). Fecha de la última modificación del catálogo. *Formato ISO 8601 (yyyy-MM-ddThh\:mm\:ss.fffffff)*.
- **`Providers`**: (``list``). Array de proveedores.
    - **`ProviderId`**: (``string``). Identificador del proveedor. Alfanumérico de 13 caracteres.
    - **`ProviderName`**: (``string``). Nombre del proveedor.
    - **`ProviderDescription`**: (``string``). Descripciones del proveedor.
    - **`ProviderCommercialConditions`**: (``string``) ``Opcional``. Condiciones comerciales de proveedor. Si no existen, este campo no se mostrará.
    - **`ProviderAccessConditions`**: (``string``) ``Opcional``. Condiciones de acceso del proveedor. Si no existen, este campo no se mostrará.
    - **`ExchangeVoucherPoint`**: (``string``) ``Opcional``. Lugar en el que las entradas puedes ser usadas o canjeadas.
    - **`AdvancedDateSelectorMethodName`**: (``string``) ``Opcional``. Nombre del método que define si los tickets de un producto pueden tener su propia fecha de acceso particular.

        ??? example "Posibles valores"
            --8<-- "includes/annex/advancedDateSelector.es.md"

    - **`CancellationPolicy`**: (``object``) ``Opcional``. Indica las políticas de cancelación que se aplican al cancelar una venta de este proveedor. Si un producto concreto no tiene políticas de cancelación se aplicarán estas.
        - **`IsRefundable`**: (``boolean``). Indica si el cliente puede cancelar gratis en algún momento.
        - **`Rules`**:  (``list``). Reglas que se aplican al efectuar la cancelación.
            - **``(object)``**: Tramos de cancelación.
                - **`HoursInAdvanceOfAccess`**: (``decimal``). Indica la cantidad de horas de antelación con respecto a la fecha de acceso a partir de las cuales se aplicará la penalización de precio indicada en `Percentage`.
                - **`Percentage`**: (``decimal``). Porcentaje de penalización sobre el precio de la entrada.
    - **`DemandAccessDate`**: (``boolean``). Indica si la fecha de acceso es necesaria. En caso de no ser necesaria, al añadir el producto al carrito debe usarse la fecha de compra.
    - **`TaxType`**: (``byte``). Indica el tipo de impuesto de los productos del proveedor.

        ??? example "Posibles valores"
            - 0: IVA
            - 1: IGIC

    - **`Type`**: (``byte``). Indica el tipo de proveedor. Por defecto será 0.

        ??? example "Posibles valores"
            - 0: Actividad
            - 1: Alojamiento
            - 2: Transporte

    - **`DemandAccessDateOnOpenDate`**: (``boolean``). Si el producto es de fecha abierta, este parámetro determinará, con verdadero o falso, la necesidad de pedir las fechas de acceso.

    - **`PurchaseFlowType`**: (``byte``). Indica el tipo de flujo de venta que tiene el proveedor. Sirve para saber si las entradas y los códigos de acceso estarán disponibles en el momento de la compra o posteriormente.

        ??? example "Posibles valores"
            - 1: Venta libre.
            - 2: Requiere tramitación por parte del proveedor.

    - **`IsForGroups`**: (``boolean``). Indica si los productos del proveedor están destinados a la venta para grupos.
    - **`IsForSeasonTickets`**: (``boolean``). Indica si los productos del proveedor son abonos de temporada.
    - **`IsInsurable`**: (`boolean`) `Opcional`. Indica sí para este producto es posible añadir un seguro de cancelación.
                    
        ??? tip "Implicaciones"
            En caso de estar definido como `#!csharp true` será necesario antes de iniciar cualquier venta hacer la llamada para [comprobar pólizas disponibles](checkInsurancePolicies.md). Esta función nos devolverá un listado de polizas disponibles con sus identificadores. Si queremos añadir una de estas polizas a la venta, pasaremos dicho identificador(`Id`) de poliza en la propiedad `InsurancePolicyId` en la [Confirmación de la reserva](../shoppingCart/sale.md).
    
    - **`LimitOfNumberOfPeopleToBeGroup`**: (``int``). Límite del número de personas que conforman un producto a partir del cual la venta se considera para "grupos". Por ejemplo, si este límite es "19" y el proveedor no es para grupos (`#!csharp IsForGroups == false`), no se aceptarán ventas con 20 o más personas. Por contra, si el proveedor es para grupos (`#!csharp IsForGroups == true`), solo se aceptarán ventas para 20 o más personas.
    - **`Logo`**: (``string``). Url para descargar la imagen del logotipo del proveedor.
    - **`Tags`**: (``list``). Array de [identificadores de etiquetas](tags.md) aplicadas al proveedor.
        - **``(string)``**: Identificador de la etiqueta.
    - **`Location`**: (``object``). Información de localización.
        - **`CountryCode`**: (``string``). Código de país (es, fr...).
        - **`City`**: (``string``). Ciudad.
        - **`Address`**: (``string``). Dirección.
        - **`ZipCode`**: (``string``). Código postal.
        - **`Lat`**: (``double``). Latitud.
        - **`Lng`**: (``double``). Longitud.
        - **`Region`**: (``string``). Region.
    - **`Ticket enclosures`**: (``list``). Información de los recintos del proveedor.
        - **`TicketEnclosureId`**: (``string``). Identificador del recinto.
        - **`TicketEnclosureName`**: (``string``). Nombre del recinto.
        - **`TicketEnclosureConditions`**: (``string``) ``Opcional``. Condiciones del recinto.
        - **`TypeOfPersonDefinitionTypeChild`**: (``byte``) ``Opcional``. Indica qué atributo se aplica a la persona para considerarla niño.

            ??? example "Posibles valores"
                --8<-- "includes/annex/typeOfPersonDefinition.es.md"

        - **`TypeOfPersonDefinitionValueChild`**: (``decimal``) ``Opcional``. Indica el valor asignado al tipo de persona niño.
        - **`TypeOfPersonDefinitionTypeAdult`**: (``byte``) ``Opcional``. Indica qué atributo se aplica a la persona para considerarla adulto.

            ??? example "Posibles valores"
                --8<-- "includes/annex/typeOfPersonDefinition.es.md"

        - **`TypeOfPersonDefinitionValueAdult`**: (``decimal``) ``Opcional``. Indica el valor asignado al tipo de persona adulto.
        - **`TypeOfPersonDefinitionTypeSenior`**: (``byte``) ``Opcional``. Indica qué atributo se aplica a la persona para considerarla senior.

            ??? example "Posibles valores"
                --8<-- "includes/annex/typeOfPersonDefinition.es.md"

        - **`TypeOfPersonDefinitionValueSenior`**: (``decimal``) ``Opcional``. Indica el valor asignado al tipo de persona senior.
        - **`Sessions`**:  (``object``) ``Opcional``. Define la relación entre sesiones y contenido. Antes de continuar, es imprescindible estudiar el apartado [obtención de sesiones](sessions.md).
            - **`SessionContentProfileId`**: (``string``). Para más información acerca de este identificador, consulte la página de [sesiones](sessions.md).
            - **`SessionGroupProfileId`**: (``string``). Para más información acerca de este identificador, consulte la página de [sesiones](sessions.md).
            - **``HasSeating``**: (``boolean``). Indica si el recinto tiene asientos, en tal caso será necesario comprobar el tipo de asignación del asiento a nivel de ticket.
            - **`SessionsGroupSessionContents`**:  (``object``). Define la relación entre grupos de sesión y contenidos de sesión. Es decir, todas las sesiones del grupo de sesión tendrán asignado el contenido de sesión. `SessionsGroupSessionContents` es excluyente respecto a `SessionSessionContents`.
                - **`SessionsGroupId`**: (``string``). Identificador del grupo de sesiones.
                - **`SessionContentId`**: (``string``). Identificador de contenido de sesión.
            - **`SessionSessionContents`**: (``list``). Define la relación entre sesiones y contenidos de sesión. `SessionSessionContents` es excluyente respecto a `SessionsGroupSessionContents`.
                - **`SessionId`**: (``string``). Identificador de sesión.
                - **`SessionContentId`**: (``string``). Identificador de contenido de sesión.
                - **`SessionTime`**: (``dateTime``). Fecha y hora de la sesión.
                - **`HasLimitedCapacity`**: (``boolean``). Indica si la sesión tiene aforo. De ser así será imprescindible consultar la disponibilidad de la sesión antes de crear una venta. Más información al respecto en [obtención de aforo disponible](availability.md).
            - **`TicketEnclosureAutoAssignSessionType`**: (``byte``). Indica qué atributo se aplica a la hora de elegir sesiones. Pueden ser sesiones auto asignadas por el sistema, elegibles, o una mezcla de los dos casos. En el caso de sesiones auto asignadas se puede comprobar qué sesiones se van a asignar antes de añadir el producto al carrito mediante el [método para comprobar la sesión autoasignada](autoAssignSession.md).

                ??? example "Posibles valores"
                    --8<-- "includes/annex/autoAssignSessionType.es.md"

        - **`ProductBases`**: (``list``). Array de categorías.
            - **`ProductBaseId`**: (``string``). Identificador de la categoría. Alfanumérico de 13 caracteres.
            - **`ProductBaseName`**: (``string``). Nombre de la categoría.
            - **`ProductBaseDescription`**: (``string``). DDscripción de la categoría. Suele contener las condiciones comunes al todos sus productos.
            - **`LimitOfNumberOfPeopleToBeGroup`**: (``int``) ``Opcional``. Mismo significado que la propiedad `LimitOfNumberOfPeopleToBeGroup` en el nodo `Provider`. Si está especificado se usará el más restrictivo entre este valor y el de proveedor.
            - **`IsInsurable`**: (`boolean`) `Opcional`. Indica sí para este producto es posible añadir un seguro de cancelación.
                    
                ??? tip "Implicaciones"
                    En caso de estar definido como `#!csharp true` será necesario antes de iniciar cualquier venta hacer la llamada para [comprobar pólizas disponibles](checkInsurancePolicies.md). Esta función nos devolverá un listado de polizas disponibles con sus identificadores. Si queremos añadir una de estas polizas a la venta, pasaremos dicho identificador(`Id`) de poliza en la propiedad `InsurancePolicyId` en la [Confirmación de la reserva](../shoppingCart/sale.md).
          
            - **`Tags`**: (``list``). Array de [identificadores de etiquetas](tags.md) aplicadas a la categoría.
                - **``(string)``**: Identificador de la etiqueta.
            - **`Products`**: (``list``). Array de productos.
                - **`ProductId`**: (``string``). Identificador del producto. Alfanumérico de 13 caracteres.
                - **`ProductName`**: (``string``). Nombre del producto.
                - **`SuggestedSalesProductName`**: (``string``). Nombre sugerido del producto de cara a la venta.
                - **`ProductDescription`**: (``string``). Descripción del producto. Suele contener las condiciones del producto.
                - **`Tags`**: (``list``). Array de [identificadores de etiquetas](tags.md) aplicadas al producto.
                    - **``(string)``**: Identificador de la etiqueta.
                - **`ProductInternalConsiderations`**: (``string``). Consideraciones internas del producto que solo debe conocer el colaborador.

                    ???+ danger "Importante"
                        **NUNCA** mostrar al cliente final.

                - **`ProductCancellationConditions`**: (``string``). Condiciones de cancelación para el producto.
                - **`CancellationPolicy`**: (``object``). Indica las políticas de cancelación que se aplican al cancelar una venta de este producto. Si este nodo está presente, tiene preferencia sobre el nodo `CancellationPolicy` del proveedor.
                    - **`IsRefundable`**: (``boolean``). Indica si el cliente puede cancelar gratis en algún momento.
                    - **`Rules`**: (``list``). eglas que se aplican al efectuar la cancelación.
                    - **``(object)``**: Tramos de cancelación.
                        - **`HoursInAdvanceOfAccess`**: (``decimal``). Indica la cantidad de horas de antelación con respecto a la fecha de acceso a partir de las cuales se aplicará la penalización de precio indicada en `Percentage`.
                        - **`Percentage`**: (``decimal``). Porcentaje de penalización sobre el precio de la entrada.
                - **`StartIsActiveDate`**: (``dateTime``) ``Opcional``. Si existe, define la fecha a partir de la cual es posible vender el producto.
                - **`EndIsActiveDate`**: (``dateTime``) ``Opcional``. Si existe, define la fecha hasta la cual es posible vender el producto.
                - **`DaysWithLimitedCapacity`**: (``string``). Fechas en los que el producto tiene un aforo limitado. Por tanto, será imprescindible consultar la disponibilidad del producto antes de crear una venta. Las fechas tendrán *formato ISO 8601 (yyyy-MM-dd)*, y estarán separadas entre sí por una coma. Más información al respecto en el punto [obtención de aforo disponible](availability.md).
                - **`HoursInAdvanceOfPurchase`**: (``short``). Horas de antelación de la compra respecto a las 00:00 del día siguiente al de la visita. Por ejemplo, si un producto tiene `HoursInAdvanceOfPurchase = 4`, y un cliente realiza una compra para el 15 de Agosto, el límite de tiempo que tiene el producto para venderse son las 20:00 del propio 15 de Agosto (es decir, 4 horas antes de las 00:00 del 16 de Agosto). Esto es importante, por ejemplo, para que un cliente no compre los productos para un día cuando el recinto ya está a cerrado.
                - **`MaxHoursInAdvanceOfPurchase`**: (``dateTime``) ``Opcional``. Horas máximas de antelación de la compra respecto a las 00:00 del día siguiente al de la visita. Por ejemplo, si un producto tiene `MaxHoursInAdvanceOfPurchase = 240`, y un cliente realiza una compra para el 15 de Agosto, el producto no puede venderse antes del 6 de Agosto (es decir, 240 horas = 10 días antes de las 00:00 del 16 de Agosto). Esto es útil, por ejemplo, para limitar el período de venta de un producto a un plazo de días previos.
                - **`MinimumNumberByTransaction`**: (``int``). Cantidad mínima de productos por cada venta. Por defecto es 1. Por ejemplo, imaginemos un producto del tipo "Entrada con descuento a partir de 3 productos". En ese caso MinimumNumberByTransaction sería 3.
                - **`NumberOfPeople`**: (``int``). Número de personas que computan para considerar una venta como "grupo". Es decir, computa para el límite `LimitOfNumberOfPeopleToBeGroup`.
                - **`NumberOfAdults`**: (``byte``). Número de adultos, incluidos en el campo `NumberOfPeople`.
                - **`NumberOfBabies`**: (``byte``). Número de bebés, incluidos en el campo `NumberOfPeople`.
                - **`NumberOfChildren`**: (``byte``). Número de niños, incluidos en el campo `NumberOfPeople`.
                - **`NumberOfSenior`**: (``byte``). Número de seniors, incluidos en el campo `NumberOfPeople`.
                - **`NumberOfGeneric`**: (``byte``). Número de genéricos, incluidos en el campo `NumberOfPeople`. Es un campo muy útil, por ejemplo, si un producto vale tanto para adulto como para niño como para senior.
                - **`RequiresRealTimePrice`**: (``boolean``). Indica si el producto requiere precio en tiempo real.

                    ??? tip "Implicaciones"
                        En caso de estar definido como `#!csharp true` será necesario antes de iniciar cualquier venta hacer la llamada para [consultar el precio en tiempo real](realTimePrices.md). Ya que el precio del producto puede ser diferente en función de algunos criterios.

                - **`IsInsurable`**: (`boolean`) `Opcional`. Indica sí para este producto es posible añadir un seguro de cancelación.
                    
                    ??? tip "Implicaciones"
                        En caso de estar definido como `#!csharp true` será necesario antes de iniciar cualquier venta hacer la llamada para [comprobar pólizas disponibles](checkInsurancePolicies.md). Esta función nos devolverá un listado de polizas disponibles con sus identificadores. Si queremos añadir una de estas polizas a la venta, pasaremos dicho identificador(`Id`) de poliza en la propiedad `InsurancePolicyId` en la [Confirmación de la reserva](../shoppingCart/sale.md).

                - **``IsForPackaging``**: (``boolean``). Indica si el producto requiere ser empaquetado, por ejemplo, con alojamiento.
                - **`ValidDays`**: (``int``). Días de validez.
                - **`ValidDaysType`**: (``byte``). Tipo de días válidos.

                    ??? example "Posibles valores"
                        - 0: consecutivos.
                        - 1: no consecutivos.

                - **`PriceMode`**: (``byte``). Indica el tipo de precio.

                    ??? example "Posibles valores"
                        - 1: PVP.
                        - 2: precio neto.

                - **`Commission`**: (``list``). En caso de que `PriceMode = PVP`, nos indica la comisión.
                    - **`Type`**: (``int``). ndica el tipo de comisión aplicada.

                        ??? example "Posibles valores"
                            - 1: porcentaje.
                            - 2: valor absoluto.

                    - **`Value`**: (``decimal``). valor de esa comisión.

                        ??? info "Ejemplo"
                            - si `Type = 1` y `Value = 10`, indica que la comisión es del 10% respecto al `Price` del producto. Es decir, si el `Price` es igual a 100€, la comisión calculada sería de 10€.
                            - si `Type = 2` y `Value = 3`, indica que la comisión por producto es de 3€.

                - **`AccessDateCriteria`**: (``byte``). Indica el criterio para la fecha de acceso.

                    ??? example "Posibles valores"
                        --8<-- "includes/annex/accessDateCriteria.es.md"

                - **`BarcodeAssignment`**: (``byte``) ``Opcional``. Indica a qué se va a asignar el código de barras.

                    ??? example "Posibles valores"
                        - 1: Ticket (valor por defecto si `BarcodeAssignment` no viene definido).
                        - 2: Persona.

                        ???+ info "Ejemplo"
                            El producto "Entrada dos días" compuesto por un adulto y 2 tickets (entrada día 1, entrada día 2):

                            - `BarcodeAssignment = Ticket`: cada uno de los tickets tendrá su propio código de barras.
                            - `BarcodeAssignment = Persona`: solo habrá un código de barras (compartido por ambos tickets). Una consecuencia directa de este caso la tendríamos a la hora de imprimir un PDF con las entradas, ya que solo tendríamos que imprimir un PDF del producto, dado que a pesar de tener dos tickets solo hay un código de barras.

                - **`PricesAndDates`**: (``list``). Array de "*precio y fechas*". Tiene una doble funcionalidad. Por una parte nos define qué fechas de acceso tiene disponible el producto, y por otra parte nos define qué precio se aplica a qué fechas.
                    - **`Price`**: (``decimal``). Precio.
                    - **`Currency`**: (``string``). Moneda.
                    - **`CurrencyName`**: (``string``). Nombre de la moneda.
                    - **`Dates`**: (``string``). Las fechas tendrán *formato ISO 8601 (yyyy-MM-dd)* y estarán separadas entre sí por una coma.
                    - **`OriginalPrice`**:  (``decimal``) ``Opcional``. Precio del producto antes de aplicar descuentos si existen.
                    - **`TaxBreakdown`**: (``list``). Array con el desglose de impuestos.
                        - **`TaxPercentage`**: (``decimal``). Porcentaje de impuesto (sobre 100).
                        - **`PriceWithoutTaxes`**: (``decimal``). Precio sin impuestos.
                        - **`PriceWithTaxes`**: (``decimal``) Precio con impuestos.
                - **`Release`**: (``short``) ``Opcional``. Número de días de antelación necesarios para que el cliente pueda cancelar el producto sin coste.

                    ??? info "Ejemplo"
                        - 0: El cliente puede cancelar el día de entrada al parque sin coste.
                        - 1: El cliente puede cancelar un día antes de la entrada al parque sin coste.

                - **`SalesDocumentSettings`**: (``object``). Configuraciones respecto al documento de acceso (pdf, passbook). Esta información también vendrá como resultado al confirmar una venta.

                    ??? tip "Consejo"
                        Si se utilizan los documentos generados por nosotros no será necesario tener en cuenta estas configuraciones. De lo contrario, debéis tenerlas en consideración.

                    - **`Disable`**: (``boolean``). Indica si no se generará documento de acceso para este producto.
                    - **`ShowPrice`**: (``boolean``). Indica si se debe mostrar el precio en el documento de acceso.
                    - **`AccessDateCriteriaOpenDateSalesDocument`**: (``int``) ``Opcional``. Sólo en el caso de que `AccessDateCriteria == 1` (fecha abierta). Indica qué debemos informar al cliente respecto a la fecha de acceso.

                        ??? example "Posibles valores de AccessDateCriteria y AccessDateCriteriaOpenDateSalesDocument"
                            --8<-- "includes/annex/accessDateCriteria.es.md"

                - **`HasSaleFlowRules`**: (``boolean``). Indica si el producto tiene alguna regla asociada de flujo de venta. En el caso de ser ``#!csharp true`` se recomienda consultar el método [Comprobar reglas de flujo de venta](checkSaleFlowRules.md) para comprobar qué cambios va a producir la inclusión de este producto a la hora de añadirlo al carrito.
                - **`Tickets`**: (``list``) ``Opcional``. Array de tickets. En caso de que el producto no trabaje con tickets, este campo no existirá.
                    - **`TicketId`**: (``string``). Identificador de ticket. Alfanumérico de 13 caracteres.
                    - **`IsQuotaTicket`**: (``boolean``). Booleano que indica si el ticket es o no de tipo aforo, lo que quiere decir que en caso de ser `#!csharp true` el ticket computará para el total de aforo necesario para reservar el producto. Por ejemplo, si tenemos un producto donde tiene 3 tickets definidos pero únicamente 2 de ellos son de tipo aforo, entonces al consultar la disponibilidad para esté producto hay que tener en cuenta que a nivel de aforo necesita 2 de disponibilidad. En otras palabras en caso de que el aforo disponible fuese 1 no podríamos reservar este producto. Para más información consulta el endpoint [obtención de aforo disponible](availability.md).
                    - **`TicketName`**: (``string``). Nombre del ticket.
                    - **`TicketConditions`**: (``string``) ``Opcional``. Condiciones del ticket.
                    - **`TicketEnclosureId`**: (``string``). Identificador del recinto al que pertenece el ticket. Varios tickets puede pertenecer al mismo recinto.
                    - **``SeatingAssignType``**: (``byte``). Indica el tipo de asignación de asiento que aplica.

                        ??? example "Posibles valores"
                            - 1: **Auto asignados**, los asientos serán asignados automáticamente por el sistema.
                            - 3: **Requiere procesamiento**, los asientos serán asignados posteriormente por el proveedor.

                    - **`TicketsQuestionsProfileId`**: (``string``) Identificador del perfil de una pregunta.
                    - **`FromAccessDay`** y **`ToAccessDay`**: (``byte``). Si están definidos, indican para qué días respecto a la primera fecha de acceso es válido el ticket.

                        ???+ tip "Consejo"
                            El resultado de la llamada para confirmar una venta ya nos devuelve el rango de fechas de acceso de cada ticket. Por tanto es totalmente factible no tratar `FromAccessDay` y `ToAccessDay` y basarnos en lo que nos devuelva dicha llamada.

                        ??? info "Ejemplo"

                            - Si el ticket define FromAccessDay = 1 y ToAccessDate = 1, el cliente deberá usarlo el primer día de acceso.
                            - Si el ticket define FromAccessDay = 2 y ToAccessDate = 2, el cliente deberá usarlo el segundo día de acceso.
                            - Si el ticket define FromAccessDay = 1 y ToAccessDate = 2, el cliente podrá entrar o el primer o el segundo día.
                            - Si el ticket define FromAccessDay = 2 y ToAccessDate no definido, el cliente podrá entrar desde el segundo día hasta un día indefinido, por ejemplo hasta que termine la temporada, *salvo que las condiciones del producto indiquen lo contrario*.
                            - Si el ticket no define ni FromAccessDay ni ToAccessDate, el cliente solo podrá entrar el primer día, *salvo que se indique lo contrario en las condiciones*.

                    - **`TypeOfPerson`**: (``list``) ``Opcional``. Define el tipo de persona y su numeración.
                        - **`Type`**:  (``byte``). Indica el tipo de persona.

                            ??? example "Posibles valores"
                                - 1: Bebé
                                - 2: Niño
                                - 3: Adulto
                                - 4: Senior
                                - 5: Genérico

                        - **`PersonNumber`**: (``byte``). Identificador del número de persona por tipo.

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

                    - **``RequiresDeliveryManagement``**: (``boolean``). Indica si es un ticket que requiere de entrega física. En caso afirmativo, habrá que elegir el método de entrega al añadir el producto al carrito. Puede consultar los métodos de entrega disponibles en el apartado [Obtener Métodos de entrega](deliveryMethods.md).

                - **`ProductPaxGroupingId`**: (``string``) ``Opcional``. Identificador de la agrupación de productos a la que pertenece el producto.

        - **`ProductPaxGroupings`**: (``list``). Agrupaciones de productos cuya diferencia principal son las personas que lo componen.
            - **`ProductPaxGroupingId`**: (``string``). Identificador de la agrupación. Alfanumérico de 13 caracteres.
            - **`ProductPaxGroupingName`**: (``string``). Nombre de la agrupación.

    - **`Urls`**: (``list``) ``Opcional``. Array de urls para acceder a la página de la taquilla del proveedor. Sólo en el caso de tener DNS personalizadas.
        - **`LanguageCode`**: (``string``). Código del idioma con el que se va a acceder. Representado mediante el *formato ISO 639-1*.
        - **`Url`**: (``string``). Url de acceso.

- **`CombinedProducts`**: (``list``). Array de productos combinados.
    - **`CombinedProductId`**: (``string``). Identificador de producto combinado.
    - **`Name`**: (``string``). Nombre del producto combinado.
    - **`PriceFrom`**: (``decimal``). Precio "*desde*" para el producto combinado.
    - **`PriceTo`**: (``decimal``). Precio "*hasta*" para el producto combinado.
    - **`Products`**: (``list``). Array de productos que forman parte del producto combinado.
        - **`ProductId`**: (``string``). Identificador del producto.
    - **`RequiresRealTimePrice`**: (``boolean``). Indica si requiere consultar el precio en tiempo real para el producto combinado. Véase [obtención del precio en tiempo real](realTimePrices.md)
- **`SaleFlowRules`**: (``object``). 
    - **`HasSaleFlowRules`**: (``boolean``). Indica si hay productos que tengan alguna regla asociada de flujo de venta. En el caso de ser ``#!csharp true`` se recomienda consultar el método [Comprobar reglas de flujo de venta](checkSaleFlowRules.md) para comprobar qué cambios va a producir la inclusión de este producto a la hora de añadirlo al carrito.
    - **`ProductIdsWithSaleFlowRules`**: (``list``). Array de identificadores de productos. Indica qué productos del catálogo tienen alguna regla asociada de flujo de venta.
    - **`DynamicProviderIdsWithSaleFlowRules`**: (``list``). Array de identificadores de proveedores dinámicos. Indica qué proveedores dinámicos del catálogo tienen alguna regla asociada de flujo de venta.
- **`PartnerSettings`**: (``object``). Indica las configuraciones del colaborador.
    - **`DemandClientData`**: (``boolean``). Valor de verdad `#!csharp true/false` que indica si es obligatorio indicar datos del cliente al confirmar una venta.
    - **`DemandClientTaxData`**: (``boolean``). Valor de verdad `#!csharp true/false` que indica si es obligatorio indicar los datos fiscales del cliente al confirmar una venta.
    - **`EnableCancellationRequest`**: (``boolean``). Valor de verdad `#!csharp true/false` que indica si el colaborador tiene permitido solicitar cancelaciones vía API.
    - **`IsInsurancePolicyEnabled`**: (``boolean``). Valor de verdad `#!csharp true/false` que indica si el colaborador tiene disponible [pólizas de seguro](checkInsurancePolicies.md).
    - **`PaymentType`**: (``byte``). Indica el tipo de pago que realiza el colaborador.

        ??? example "Posibles valores"
            - 1: Débito
            - 2: Crédito
            - 3: Crédito excepto para grupos
            - 4: Prepago

--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/catalogResponseExamples.md"
