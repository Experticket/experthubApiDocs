# Comprobar sesiones auto asignadas

Existen ciertos productos cuyas sesiones no pueden ser elegidas explícitamente, es el sistema el que auto asigna las sesiones según la disponibilidad.

Para saber si un producto tiene sesiones auto asignadas, se comprueba mirando en el [catálogo](catalog.md) la propiedad [TicketEnclosureAutoAssignSessionType](catalog.md#estructura-de-datos-de-respuesta) del nodo de sesiones de un recinto.

Una vez lanza la consulta se devolverá, a modo informativo, las sesiones ue se auto asignarán cuando se realice el proceso de reserva.

## Método de acceso

**POST** /autoassignsessions

## Estructura de datos de envío

- **`LanguageCode`**: define el idioma en que se mostrarán los textos.

    ??? example "Posibles valores"
        - es
        - en
        - fr
        - it

- **`Products`**: lista de productos para los que se quieren comprobar las sesiones.
    - **`ProductId`**: identificador del producto.
    - **`Quantity`**: cantidad.
    - **`AccessDate`**: fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **`Tickets`**: lista de tickets para los que queremos comprobar la auto asignación.
        - **`TicketId`**: identificador del ticket.
        - **`AccessDate`**: (opcional) si se indica, tiene preferencia sobre la fecha indicada a nivel de producto. *Formato ISO 8601 (yyyy-MM-dd)*.

### Ejemplo de envío

En el siguiente ejemplo vamos a comprobar las sesiones auto asignadas para un producto con sesiones disponibles y otro sin sesiones disponibles.

--8<-- "includes/AutoAssignSessionQueryExamples.md"

``` json
{
    "Products": [
        {
            "ProductId": "hwuk9huaqopwo",
            "Quantity": 4,
            "AccessDate": "2021-06-02",
            "Tickets": [
                {
                    "TicketId": "654e5ytetr"
                }
            ]
        },
        {
            "ProductId": "6asd55fa6s5f",
            "Quantity": 4,
            "AccessDate": "2021-06-02",
            "Tickets": [
                {
                    "TicketId": "uy456i4yu6"
                }
            ]
        }
    ]
}
```

## Estructura de datos de respuesta

- **`Products`**: array que contiene los productos solicitados.
    - **`ProductId`**: identificador del producto.
    - **`AccessDate`**: fecha de acceso del producto. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **`HasTicketEnclosures`**: booleano que indica si el producto tiene recintos.
    - **`Tickets`**: array de los tickets solicitados del producto.
        - **`TicketId`**: identificador del ticket.
        - **`AccessDate`**: fecha de acceso del ticket. *Formato ISO 8601 (yyyy-MM-dd)*.
        - **`TicketEnclosureId`**: identificador del recinto.
        - **`SessionId`**: identificador de la sesión asignada.
        - **`SessionTime`**: hora de la sesión asignada en caso de haber podido asignar alguna.
        - **`SessionContentId`**: identificador del contenido de sesión.
        - **`SessionContentName`**: nombre del contenido de sesión.
        - **`ResultType`**: atributo que indica el resultado de la auto asignación.

            ??? example "Posibles valores"
                Para definir el criterio de acceso utilizamos atributos de tipo entero, pudiendo tomar los siguientes valores:
                
                - `Ok`. Auto asignación correcta: 0.
                - `HasNotTicketEnclosure`. El producto no tiene recintos, por lo tanto es un producto sin sesiones: 1.
                - `TicketEnclosureSessionTypeIsNone`. El producto no tiene sesiones en ninguno de sus recintos: 2.
                - `TicketEnclosureDoesNotAcceptAutoAssign`. El producto no tiene recintos con sesiones configuradas como auto asignables: 3.
                - `TicketEnclosureHasNoSessionsAvailable`. No hay sesiones disponibles para el producto y fecha seleccionados: 4.

- **`Timestamp`**.
- **`ErrorMessage`**: mensaje de error explicando por qué la obtención de las sesiones no ha sido correcta. En caso que haya sido correcta, el campo no aparece.

### Ejemplo de respuesta

--8<-- "includes/AutoAssignSessionResultExamples.md"

``` json
{
    "Products": [
        {
            "ProductId": "hwuk9huaqopwo",
            "AccessDate": "2021-06-02",
            "HasTicketEnclosures": true,
            "Tickets": [
                {
                    "TicketId": "654e5ytetr",
                    "AccessDate": "2021-06-02",
                    "TicketEnclosureId": "09aslkdfj354",
                    "SessionId": "lksdgjj4235",
                    "SessionTime": "18:00",
                    "SessionContentId": "nljkasdfjlk87",
                    "SessionContentName": "Viaje al centro de la tierra",
                    "ResultType": 0
                }
            ]
        },
        {
            "ProductId": "6asd55fa6s5f",
            "AccessDate": "2021-06-02",
            "HasTicketEnclosures": true,
            "Tickets": [
                {
                    "TicketId": "uy456i4yu654i",
                    "AccessDate": "2021-06-02",
                    "TicketEnclosureId": "09aslkdfj354",
                    "SessionId": "999tre44143",
                    "SessionContentId": "xcmnbvhasd00",
                    "SessionContentName": "Robinson Crusoe",
                    "ResultType": 0
                }
            ]
        }
    ],
    "Success": true,
    "Timestamp": "2022-02-18T17:02:27.8165916"
}
```
