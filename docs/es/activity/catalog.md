# Obtención del catálogo de actividades

En un primer paso, tendrá que obtener todo el catálogo completo de proveedores, categorías (productBases) y productos para su tratamiento interno.

La información del catálogo incluye los identificadores únicos de Proveedor, Producto y Ticket que posteriormente se usarán para añadir cualquier producto al carrito.

También incluirá otros datos como el precio de los productos dependiendo de las fechas, o las condiciones comerciales del producto.

Siguiendo con nuestro ejemplo, podría darse el caso de que el producto "Entrada 2x1 Niño" del proveedor PAC baje el precio y aumente el periodo de validez de la venta.

## Método de acceso

**POST** /activity/catalog

## Estructura de datos de envío

Para obtener el catálogo podemos utilizar diferentes filtros en el body del método.

Cada filtro se considerará un ***AND***. Por ejemplo, pueden filtrarse por varios *ProductIds* pero no tiene sentido filtrar por *ProviderIds* y por *ProductIds* siendo este último de un proveedor diferente.

- **`ProviderIds`**: `#!csharp List<string>` lista identificadores de proveedor.
- **`ProductBaseIds`**: `#!csharp List<string>` lista identificadores de categoría.
- **`ProductIds`**: `#!csharp List<string>` lista identificadores de producto.
- **`FromDate`**: `#!csharp string` fecha de inicio. No permite valores menores al día actual. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`ToDate`**: `#!csharp string` fecha de fin. Por defecto su valor es el de la fecha correspondiente a dentro de un año. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`ReferenceDate`**: `#!csharp string` exige que el día que se tome como referencia para el cálculo de precios y disponibilidades no sea hoy, sino el indicado. Por ejemplo se usará si los precios cambian dependiendo de los días que quedan hasta la fecha de la entrada. *Formato ISO 8601 (yyyy-MM-dd)*
- **`LanguageCode`**: `#!csharp string` define el idioma en que se mostrarán los textos del catálogo (nombre/descripción/condiciones de proveedor/producto/). Por defecto se devolverá el idioma configurado para el  colaborador.
- **`ShowProductsOutOfActiveDateRange`**: `#!csharp bool` si su valor es `#!csharp true`, la respuesta devolverá productos en los que el día de hoy (o el día indicado en ReferenceDate) está fuera de su rango de fechas de venta. Por ejemplo, si estamos en diciembre y hay productos que se pueden vender a partir de enero, poniendo este valor a true nos permitirá descubrir que existen esos productos.

### Ejemplos

--8<-- "includes/CatalogQueryExamples.md"

## Estructura de datos de respuesta

- **`LastUpdatedDateTime`**: Fecha de la última modificación del catálogo.
- **`Providers`**: Array de proveedores:
  - **`ProviderId`**: Identificador del proveedor. Alfanumérico de 13 caracteres (por ejemplo "by81fymhsmjgw").
  - **`ProviderName`**: Nombre del Proveedor (por ejemplo "PTM").
  - **`ProviderDescription`**: Descripciones del proveedor.
  - **`ProviderCommercialConditions`**: Condiciones comerciales de proveedor. Si no existen, este campo no se mostrará.
  - **`ProviderAccessConditions`**: Condiciones de acceso del proveedor. Si no existen, este campo no se mostrará.
  - **`AdvancedDateSelectorMethodName`**: nombre del método que define si los tickets de un producto pueden tener su propia fecha de acceso particular. Más información de este punto en el Anexo II.
  - **`CancellationPolicy`**: indica las políticas de cancelación que se aplican al cancelar una venta de este proveedor. Si un producto concreto no tiene políticas de cancelación se aplicarán estas.
    - **`IsRefundable`**: indica si el cliente puede cancelar gratis en algún momento.
    - **`Rules`**: reglas que se aplican al efectuar la cancelación.
      - **`HoursInAdvanceOfAccess`**: indica la cantidad de horas de antelación con respecto a la fecha de acceso a partir de las cuales se aplicará la penalización de precio indicada en Percentage.
      - **`Percentage`**: porcentaje de penalización sobre el precio de la entrada.
  - **`DemandAccessDate`**: indica si la fecha de acceso es necesaria. En caso de no ser necesaria tanto en los métodos "Reservation" como "Transaction" debe usarse la fecha de compra.
  - **`TaxType`**: indica el tipo de impuesto de los productos del proveedor. Opciones:

    0. IVA
    1. IGIC

  - **`Type`**: indica el tipo de proveedor. Opciones:

    0. Actividad
    1. Alojamiento
    2. Transporte

  - **`IsForGroups`**: indica si los productos del proveedor están destinados a la venta para grupos.
  - **`LimitOfNumberOfPeopleToBeGroup`**: límite del número de personas que conforman un producto a partir del cual la transacción se considera para "grupos". Por ejemplo, si este límite es "19" y el proveedor no es para grupos (IsForGroups == false), no se aceptarán transacciones con 20 o más personas. Por contra, si el proveedor es para grupos (IsForGroups == true), solo se aceptarán transacciones para 20 o más personas.
  - **`Logo`**: Url para descargar la imagen del logotipo del proveedor
  - **`Location`**: Información de localización.
    - **`CountryCode`**: Código de país (es, fr...).
    - **`City`**: Ciudad.
    - **`Address`**: Dirección.
    - **`ZipCode`**: Código postal.
    - **`Lat`**: Latitud.
    - **`Lng`**: Longitud.
  - **`Ticket enclosures`**: Información de los recintos del proveedor.
    - **`TicketEnclosureId`**: Idenfificador del recinto.
    - **`TicketEnclosureName`**: Nombre del recinto.
    - **`TicketEnclosureConditions`**: [Opcional] Condiciones del recinto.
    - **`TypeOfPersonDefinitionTypeChild`**: [Opcional] Indica qué atributo * se aplica a la persona para considerarla niño.
    - **`TypeOfPersonDefinitionValueChild`**: [Opcional] Indica el valor asignado al tipo de persona niño.
    - **`TypeOfPersonDefinitionTypeAdult`**: [Opcional] Indica qué atributo * se aplica a la persona para considerarla adulto.
    - **`TypeOfPersonDefinitionValueAdult`**: [Opcional] Indica el valor asignado al tipo de persona adulto.
    - **`TypeOfPersonDefinitionTypeSenior`**: [Opcional] Indica qué atributo * se aplica a la persona para considerarla senior.
    - **`TypeOfPersonDefinitionValueSenior`**: [Opcional] Indica el valor asignado al tipo de persona senior.
    - **`Sessions`**: [Opcional] Define la relación entre sesiones y contenido. Antes de continuar, es imprescindible estudiar el apartado Obtención de sesiones:
      - **`SessionContentProfileId`**: Para más información acerca de este identificador, consulte la página de Sesiones.
      - **`SessionGroupProfileId`**: Para más información acerca de este identificador, consulte la página de Sesiones.
      - **`SessionsGroupSessionContents`**: Define la relación entre grupos de sesión y contenidos de sesión. Es decir, todas las sesiones del grupo de sesión tendrán asignado el contenido de sesión. SessionsGroupSessionContents es excluyente respecto a SessionSessionContents.
        - **`SessionsGroupId`**: Identificador del grupo de sesiones.
        - **`SessionContentId`**: Identificador de contenido de sesión.
      - **`SessionSessionContents`**: Define la relación entre sesiones y contenidos de sesión. SessionSessionContents es excluyente respecto a SessionsGroupSessionContents.
        - **`SessionId`**: Identificador de sesión.
        - **`SessionContentId`**: Identificador de contenido de sesión.
        - **`SessionTime`**: Fecha y hora de la sesión.
        - **`HasLimitedCapacity`**: Indica si la sesión tiene aforo. De ser así será imprescindible consultar la disponibilidad de la sesión antes de crear una transacción. Más información al respecto en el punto Obtención de aforo disponible.
      - **`TicketEnclosureAutoAssignSessionType`**: Indica qué atributo*** se aplica a la hora de elegir sesiones. Pueden ser sesiones auto asignadas por el sistema, elegibles, o una mezcla de los dos casos. En el caso de sesiones auto asignadas se puede comprobar qué sesiones se van a asignar antes de hacer la reserva mediante el método AutoAssignSessions.
    - **`ProductBases`**: Array de ProductBases.
      - **`ProductBaseId`**: Identificador del ProductBase. Alfanumérico de 13 caracteres (por ejemplo "htpdj798ek8ja")
      - **`ProductBaseName`**: Nombre del ProductBase.
      - **`ProductBaseDescription`**: Descripción del ProductBase. Suele contener las condiciones comunes al todos sus productos.
      - **`DaysWithLimitedCapacity`**: Fechas en los que todos los productos de este ProductBase tienen un aforo limitado. Por tanto, será imprescindible consultar la disponibilidad del ProductBase antes de crear una transacción. Las fechas tendrán formato ISO 8601 (yyyy-MM-dd), y estarán separadas entre sí por una coma. Más información al respecto en el punto Obtención de aforo disponible.
      - **`LimitOfNumberOfPeopleToBeGroup`**: (Opcional) mismo significado que la propiedad LimitOfNumberOfPeopleToBeGroup en el nodo "Provider". Si está especificado se usará el más restrictivo entre este valor y el de proveedor.
      - **`Products`**: Array de productos:
        - **`ProductId`**: Identificador del producto. Alfanumérico de 13 caracteres (por ejemplo "ctgyir9m9q4bo").
        - **`ProductName`**: Nombre del producto.
        - **`SuggestedSalesProductName`**: Nombre sugerido del producto de cara a la venta.
        - **`ProductDescription`**: Descripción del producto. Suele contener las condiciones del producto.
        - **`ProductInternalConsiderations`**: Consideraciones internas del producto que solo debe conocer Test It. NUNCA mostrar al cliente final.
        - **`ProductCancellationConditions`**: Condiciones de cancelación para el producto.
        - **`CancellationPolicy`**: indica las políticas de cancelación que se aplican al cancelar una venta de este producto. Si este nodo está presente, tiene preferencia sobre el nodo CancellationPolicy del proveedor.
          - **`IsRefundable`**: indica si el cliente puede cancelar gratis en algún momento.
          - **`Rules`**: reglas que se aplican al efectuar la cancelación.
            - **`HoursInAdvanceOfAccess`**: indica la cantidad de horas de antelación con respecto a la fecha de acceso a partir de las cuales se aplicará la penalización de precio indicada en Percentage.
            - **`Percentage`**: porcentaje de penalización sobre el precio de la entrada.
        - **`StartIsActiveDate`**: [Opcional] Si existe, define la fecha a partir de la cual es posible vender el producto.
        - **`EndIsActiveDate`**: [Opcional] Si existe, define la fecha hasta la cual es posible vender el producto.
        - **`DaysWithLimitedCapacity`**: Fechas en los que el producto tienen un aforo limitado. Por tanto, será imprescindible consultar la disponibilidad del producto antes de crear una transacción. Las fechas tendrán formato ISO 8601 (yyyy-MM-dd), y estarán separadas entre sí por una coma. Más información al respecto en el punto Obtención de aforo disponible.
        - **`HoursInAdvanceOfPurchase`**: Horas de antelación de la compra respecto a las 00:00 del día siguiente al de la visita. Por ejemplo, si un producto tiene HoursInAdvanceOfPurchase = 4, y un cliente realiza una compra para el 15 de Agosto, el límite de tiempo que tiene el producto para venderse son las 20:00 del propio 15 de Agosto (es decir, 4 horas antes de las 00:00 del 16 de Agosto). Esto es importante, por ejemplo, para que un cliente no compre los productos para un día cuando el recinto ya está a cerrado.
        - **`MaxHoursInAdvanceOfPurchase`**: [Opcional] Horas máximas de antelación de la compra respecto a las 00:00 del día siguiente al de la visita. Por ejemplo, si un producto tiene MaxHoursInAdvanceOfPurchase = 240, y un cliente realiza una compra para el 15 de Agosto, el producto no puede venderse antes del 6 de Agosto (es decir, 240 horas = 10 días antes de las 00:00 del 16 de Agosto). Esto es útil, por ejemplo, para limitar el período de venta de un producto a un plazo de días previos.
        - **`MinimumNumberByTransaction`**: Cantidad mínima del productos por cada venta. Por defecto es 1. Por ejemplo, imaginemos un producto del tipo "Entrada con descuento a partir de 3 productos". En ese caso MinimumNumberByTransaction sería 3.
        - **`NumberOfPeople`**: Número de personas que computan para considerar una transacción como "grupo". Es decir, computa para el límite "LimitOfNumberOfPeopleToBeGroup".
        - **`NumberOfAdults`**: Número de adultos, incluidos en el campo "NumberOfPeople".
        - **`NumberOfBabies`**: Número de bebés, incluidos en el campo "NumberOfPeople".
        - **`NumberOfChildren`**: Número de niños, incluidos en el campo "NumberOfPeople".
        - **`NumberOfSenior`**: Número de seniors, incluidos en el campo "NumberOfPeople".
        - **`NumberOfGeneric`**: Número de genéricos, incluidos en el campo "NumberOfPeople". Es un campo muy útil, por ejemplo, si un producto vale tanto para adulto como para niño como para senior.
        - **`RequiresRealTimePrice`**: Indica si el producto requiere precio en tiempo real.
        - **`ValidDays`**: Días de validez:

            0. consecutivos.
            1. no consecutivos.

        - **`PriceMode`**: 1 = PVP. 2 = Precio Neto.
        - **`Commission`**: En caso de que PriceMode = PVP, nos indica la comisión:
          - **`Type`**: 1 = porcentaje. 2 = valor absoluto.
          - **`Value`**: Valor de esa comisión. Por ejemplo:
            - si Type = 1 y Value = 10, indica que la comisión es del 10% respecto al Price del producto. Es decir, si el Price = 100 €, la comisión calculada sería de 10 €.
            - si Type = 2 y Value = 3, indica que la comisión por producto es de 3 €.
        - **`AccessDateCriteria`**: Indica el criterio para la fecha de acceso. Puede tomar los siguientes valores **.
        - **`BarcodeAssignment`**: [Opcional] Indica a qué se va asignar el código de barras. Sus posibles valores son:

          1. Ticket (valor por defecto si BarcodeAssignment no viene definido)
          2. Persona

                Por ejemplo, producto "Entrada dos días" compuesto por un adulto y 2 tickets (entrada día 1, entrada día 2).

                    - Si BarcodeAssignment = Ticket, cada uno de los tickets tendrá su propio código de barras
                    - Si BarcodeAssignment = Persona, solo habrá un código de barras (compartido por ambos tickets). Una consecuencia directa de este caso la tendríamos a la hora de imprimir un PDF con las entradas: solo tendríamos que imprimir un PDF del producto, dado que a pesar de tener dos tickets solo hay un código de barras.

        - **`PricesAndDates`**: Array de "precio y fechas". Tiene una doble funcionalidad. Por una parte nos define qué fechas de acceso tiene disponible el producto, y por otra parte nos define qué precio se aplican a qué fechas:
          - **`Price`**: Precio.
          - **`Currency`**: Moneda del precio.
          - **`CurrencyName`**: Nombre de la moneda del precio
          - **`Dates`**: Fechas separadas por comas. Las fechas tendrán formato ISO 8601 (yyyy-MM-dd), y estarán separadas entre sí por una coma.
          - **`OriginalPrice`**: [Opcional] Precio del producto antes de aplicar descuentos si existen.
          - **`TaxBreakdown`**: Array con el desglose de impuestos.
            - **`TaxPercentage`**: Porcentaje de impuesto (sobre 100)
            - **`PriceWithoutTaxes`**: Precio sin impuestos
            - **`PriceWithTaxes`**: Precio con impuestos
        - **`Release`**: [Opcional] Número de días de antelación necesarios para que el cliente pueda cancelar el producto sin coste. Ejemplos:

          1. El cliente puede cancelar el día de entrada al parque sin coste.
          2. El cliente puede cancelar un día antes de la entrada al parque sin coste.

        - **`SalesDocumentSettings`**: Configuraciones respecto al documento de acceso (pdf, passbook). Esta información también vendrá como resultado de la llamada al método del API "transaction". Si Test It utiliza los documentos generados por Tixalia PRE no será necesario tener en cuenta estas configuraciones. De lo contrario, si Test It genera sus propios documentos debe tenerlas en consideración.
          - **`Disable`**: Indica si no se generará documento de acceso para este producto.
          - **`ShowPrice`**: Indica si se debe mostrar el precio en el documento de acceso.
          - **`AccessDateCriteriaOpenDateSalesDocument`**: Solo en el caso de que AccessDateCriteria == 1 (Fecha Abierta). Indica qué debemos informar al cliente respecto a la fecha de acceso. Puede tomar los siguientes valores **.
        - **`Tickets`**: [Opcional] Array de tickets. En caso de que el producto no trabaje con tickets, este campo no existirá:
          - **`TicketId`**: Identificador de ticket. Alfanumérico de 13 caracteres (por ejemplo "1tqgtrf7ctefc").
          - **`IsQuotaTicket`**: Booleano que indica si el ticket es o no de tipo aforo, lo que quiere decir que en caso de ser true el ticket computará para el total de aforo necesario para reservar el producto. Por ejemplo, si tenemos un producto donde tiene 3 tickets definidos pero únicamente 2 de ellos son de tipo aforo, entonces al consultar la disponibilidad para esté producto hay que tener en cuenta que a nivel de aforo necesita 2 de disponibilidad. En otras palabras en caso de que el aforo disponible fuese 1 no podríamos reservar este producto. Para más información consulta el endpoint Obtención de aforo disponible.
          - **`TicketName`**: Nombre del ticket.
          - **`TicketConditions`**: [Opcional] Condiciones del ticket.
          - **`TicketEnclosureId`**: Idenfificador del recinto al que pertenece el ticket. Varios tickets puede pertenecer al mismo recinto
          - **`FromAccessDay`** y **`ToAccessDay`**: Si están definidos, indican para qué días respecto a la primera fecha de acceso es válido el ticket. Ejemplos,
            - si el ticket define FromAccessDay = 1 y ToAccessDate = 1, el cliente deberá usarlo el primer día de acceso.
            - si el ticket define FromAccessDay = 2 y ToAccessDate = 2, el cliente deberá usarlo el segundo día de acceso.
            - si el ticket define FromAccessDay = 1 y ToAccessDate = 2, el cliente podrá entrar o el primer o el segundo día.
            - si el ticket define FromAccessDay = 2 y ToAccessDate no definido, el cliente podrá entrar desde el segundo día hasta un día indefinido (por ejemplo hasta que termine la temporada, salvo que las condiciones del producto indiquen lo contrario).
            - si el ticket no define ni FromAccessDay ni ToAccessDate, el cliente solo podrá entrar el primer día (salvo que se indique lo contrario en las condiciones).
            [NOTA: El resultado de la llamada al método del API "Transaction" ya nos devuelve el rango de fechas de acceso de cada ticket. Por tanto es totalmente factible no tratar "FromAccessDay" y "ToAccessDay" y basarnos en lo que nos devuelva el método Transaction]
          - **`TypeOfPerson`**: [Opcional] Define el tipo de persona y su numeración. La información viene dado por:
            - **`Type`**: Bebé = 1, Niño = 2, Adulto = 3, Senior = 4, Genérico = 5
            - **`PersonNumber`**:

            Por ejemplo:

              - Producto "Entrada 3x2" compuesto por dos adultos y un niño y definido por tres tickets:
                - Ticket Adulto: Adulto 1 (Type = 3, PersonNumber = 1)
                - Ticket Adulto: Adulto 2 (Type = 3, PersonNumber = 2)
                - Ticket Niño: Niño 1 (Type = 2, PersonNumber = 1)
              - Producto "Entrada 2x1 más segundo día consecutivo" compuesto por dos adultos y 4 tickets:
                - Ticket Adulto primer día: adulto 1 (Type = 3, PersonNumber = 1)
                - Ticket Adulto primer día: adulto 2 (Type = 3, PersonNumber = 2)
                - Ticket Adulto segundo día: adulto 1 (Type = 3, PersonNumber = 1)
                - Ticket Adulto segundo día: adulto 2 (Type = 3, PersonNumber = 2)
        - **`ProductPaxGroupingId`**: [Opcional] Identificador de la agrupación de productos a la que pertenece el producto.
      - **`ProductPaxGroupings`**: Agrupaciones de productos cuya diferencia principal son las personas que lo componen.
        - **`ProductPaxGroupingId`**: Identificador de la agrupación. Alfanumérico de 13 caracteres (por ejemplo "dtpdj29bek3ja").
        - **`ProductPaxGroupingName`**: Nombre de la a agrupación./li>
    - **`Urls`**: [Opcional] Array de urls para acceder a la página de la taquilla del proveedor. Sólo en el caso de que Test It tenga DNS personalizadas.
      - **`LanguageCode`**: Código del idioma con el que se va a acceder. Representado mediante el formato ISO 639-1.
      - **`Url`**: Url de acceso.
- **`CombinedProducts`**: Array de productos combinados.
  - **`CombinedProductId`**: Identificador de producto combinado.
  - **`Name`**: Identificador de producto combinado.
  - **`PriceFrom`**:. Precio "desde" para el producto combinado.
  - **`PriceTo`**: Precio "hasta" para el producto combinado.
  - **`Products`**: Array de productos que forman parte del producto combinado.
    - **`ProductId`**: Identificador del producto.
  - **`RequiresRealTimePrice`**: Array de productos que forman parte del producto combinado.
- **`Success`**: Booleano (true/false) que indica si la obtención del catálogo ha sido o no correcta.
- **`Timestamp`**:
- **`ErrorMessage`**: Mensaje de error explicando por qué la obtención del catálogo no ha sido correcta. En caso que haya sido correcta, devolverá null.
