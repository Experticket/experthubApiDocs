# Tarjetas regalo

Podemos crear tarjetas regalo añadiendo tantas actividades del [catálogo de actividades](catalog.md) como queramos. La estructura de datos para añadir tarjetas regalo al carrito se detalla en la sección [añadir al carrito](/docs/shoppingCart/add.md).

Tras la compra de la tarjeta se genera un código único para poder canjearla. En el momento del canje es cuando se elegirán las fechas y las sesiones (si procede) de las actividades.

Para realizar el proceso de canje, los productos que componen la tarjeta se añaden al carrito indicando el código de la tarjeta regalo a la que pertenecen. La estructura de datos para indicar que una actividad pertenece a una tarjeta regalo se detalla en la sección [añadir al carrito](/docs/shoppingCart/add.md).

## Comprobar tarjeta regalo

Con este método podemos comprobar si una tarjeta regalo es canjeable a partir de un código de canje.

## Método de acceso

**GET** /activity/giftcard

## Estructura de la petición

- **``GiftCardIdentifier``**: (``string``). Código de canje.
- **`LanguageCode`**: (``string``) ``Opcional``. Define el idioma en que se mostrarán los textos. Por defecto se devolverá el idioma configurado para el colaborador.

### Ejemplo de petición

--8<-- "includes/examples/activity/giftCardQueryExamples.md"

## Estructura de la respuesta

- **``GiftCardIdentifier``**: (``string``). Código de canje.
- **``SaleId``**: (``string``). Identificador de la venta.
- **``PartnerSaleId``**: (``string``). Identificador del colaborador.
- **`IsExchanged`**: (`boolean`). Indica si la tarjeta ya ha sido canjeada.
- **`HoursInAdvanceOfGiftCardExchange`**: (``short``). Horas de antelación del canje respecto a las 00:00 del día siguiente al de la visita. Por ejemplo, si una tarjeta tiene `HoursInAdvanceOfGiftCardExchange = 4`, y un cliente realiza el canje para el 15 de Agosto, el límite de tiempo que tiene la tarjeta para canjearse son las 20:00 del propio 15 de Agosto (es decir, 4 horas antes de las 00:00 del 16 de Agosto). Esto es importante, por ejemplo, para que un cliente no canjee una tarjeta para un día cuando el recinto ya está a cerrado.
- **``Message``**: (``string``). Mensaje del comprador de la tarjeta dirigido a la persona que va a canjearla.
- **``Client``**: (``object``). Datos del cliente que va a canjear la tarjeta.
    - **`CreatedDate`**: (`dateTime`). Fecha en que se dio de alta.
    - **``FullName``**: (``string``). Nombre.
    - **``Surname``**: (``string``). Apellidos.
    - **`CountryCode`**: (`string`). Código de país.
    - **`LanguageCode`**: (`string`). Código de idioma.
    - **`Gender`**: (`byte`). Género.
    - **`AcceptsEmailContact`**: (`boolean`). Acepta recibir comunicaciones comerciales.
    - **`AllowCustomerProfiling`**: (`boolean`). Acepta la creación de un perfil de cliente.
--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/giftCardResponseExamples.md"
