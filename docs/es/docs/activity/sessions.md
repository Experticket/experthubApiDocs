# Sesiones

Una sesión está definida por una fecha, un hora, un contenido y, opcionalmente, el aforo disponible.

Según esta definición, se entiende que una misma sesión puede ser compartida por varios tickets. Los tickets "Entrada adulto", "Entrada niño", "Entrada junior", "Entrada senior" y "Entrada discapacitado" pueden tener asociadas las mismas sesiones durante el año en curso (por ejemplo, 10 sesiones al día durante los 365 días al año).

Como esta casuística puede ser habitual, se ha procurado separar lo máximo posible la estructura de sesiones del catálogo de productos. Siguiendo con el ejemplo anterior, si se definiesen las sesiones en el catálogo de productos tendríamos 10 sesiones x 365 días = 3650 sesiones para cada uno de los 5 tickets ("Entrada adulto, "Entrada niño", "Entrada junior", "Entrada senior" y "Entrada discapacitado").

Por lo tanto, se define la estructura de sesiones, para minimizar la carga de datos y jerarquizar lo mejor posible el catálogo de sesiones.

## Método de acceso

**POST** /sessions

## Estructura de datos de la petición

Para obtener las sesiones podemos utilizar diferentes filtros en el cuerpo del método. Cada filtro se considerará un ***AND***.

Debe especificarse la siguiente estructura de datos en el cuerpo del método.

- **`SessionsGroupProfileIds`**: lista de perfiles de grupos de sesión.
- **`SessionsGroupIds`**: lista de grupos de sesión.
- **`SessionContentProfileIds`**: lista de perfiles de contenido de sesión.
- **`FromDate`**: filtrado por fecha de inicio. No permite valores menores al día de hoy. El valor por defecto es el día actual. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`ToDate`**: filtrado por fecha de fin. Su valor por defecto es la fecha correnpondiente a dentro de un año. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`Dates`**: lista fechas por las que filtrar. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`LanguageCode`**: código del idioma de los contenidos.

### Ejemplos de petición

--8<-- "includes/SessionsQueryExamples.md"
=== "SessionsGroupProfileIds"

    ``` json
    {
        "SessionsGroupProfileIds": [
            "dj48vjsyufvyu",
            "ajr7v0alt62hl"
        ]
    }
    ```

=== "SessionsGroupIds"

    ``` json
    {
        "SessionsGroupProfileIds": [
            "dj48vjsyufvyu"
        ],
        "SessionsGroupIds": [
            "ajr7v0alt62hl"
        ]
    }
    ```

=== "SessionContentProfileIds"

    ``` json
    {
        "SessionsGroupProfileIds": [
            "dj48vjsyufvyu"
        ],
        "SessionsGroupIds": [
            "ajr7v0alt62hl"
        ],
        "SessionContentProfileIds": [
            "xar5v1blt61h2",
            "z2rrv6alvb2hs"
        ]
    }
    ```

---

=== "FromDate"

    ``` json
    {
        "FromDate": "2000-01-06"
    }
    ```

=== "ToDate"

    ``` json
    {
        "ToDate": "2000-01-20"
    }
    ```

=== "FromDate - ToDate"

    ``` json
    {
        "FromDate": "2000-01-06",
        "ToDate": "2000-01-20"
    }
    ```

---

=== "Dates"

    ``` json
    {
        "Dates": [
            "2000-01-06",
            "2000-05-12",
            "2000-07-21"
        ]
    }
    ```

---

=== "Combined filters"

    ``` json
    {
       "SessionsGroupProfileIds": [
           "dj48vjsyufvyu"
       ],
       "SessionsGroupIds": [
           "ajr7v0alt62hl"
       ],
       "SessionContentProfileIds": [
            "xar5v1blt61h2",
            "z2rrv6alvb2hs"
       ],
       "FromDate": "2000-01-06",
       "ToDate": "2000-10-20"
    }
    ```

## Estructura de datos de la respuesta

- **`SessionsGroupProfiles`**: array de perfiles de grupos de sesión.
    - **`SessionsGroupProfileId`**: identificador del perfil de grupos de sesión.
    - **`SessionsGroupProfileName`**: nombre del perfil de grupos de sesión.
    - **`SessionTimeAvailabilityOffset`**: cantidad de minutos antes (si el valor es negativo) o después (si el valor es positivo) en la que la sesión puede estar a la venta con respecto a la hora de la sesión.
    - **`SessionsGroups`**: array de grupos de sesiones.
        - **`SessionsGroupId`**: identificador del grupo de sesiones.
        - **`SessionsGroupName`**: nombre del grupo de sesiones.
        - **`Sessions`**: array de sesiones.
            - **`SessionId`**: identificador de la sesión.
            - **`SessionTime`**: fecha y hora de la sesión.
            - **`AvailableCapacity`**: valor que indica el aforo de la sesión. Si este campo no existe, es que no hay un aforo limitado. Si sólo se quiere consultar el aforo de una sesión, se puede utilizar el método descrito en [Obtención del aforo disponible].
- **`SessionContentProfiles`**: array de perfiles de contenidos de sesión.
    - **`SessionContentProfileId`**: identificador del perfil de contenidos de sesión.
    - **`SessionContentProfileName`**: nombre del perfil de contenidos de sesión.
    - **`SessionContents`**: array de contenidos de sesión.
        - **`SessionContentId`**: identificador del contenido de sesión.
        - **`SessionContentName`**: nombre del contenido de sesión.
        - **`SessionContentDescription`**: descripción del contenido de sesión.
- **`Success`**: booleano (true/false) que indica si la obtención de las sesiones ha sido correcta o no.
- **`Timestamp`**. *Formato ISO 8601 (yyyy-MM-ddThh:mm:ss.fffffff)*.
- **`ErrorMessage`**: mensaje de error explicando por qué la obtención de las sesiones no ha sido correcta. En caso que haya sido correcta, el campo no aparece.

### Ejemplo de respuesta

Como ejemplo, supongamos que tenemos un perfil de grupos de sesión por defecto y un perfil de contenidos de sesión por defecto.

Dentro del perfil de grupos de sesión vemos que tenemos dos grupos de sesión:

- Sesiones de mañana, que agrupa las sesiones de las 10:00h de la mañana.
- Sesiones de tarde, que agrupa las sesiones de las 17:00h de la tarde.

En el perfil de contenidos de sesión tenemos tres contenidos de sesión, que definen películas (la 1, la 2 y la 3).

Observado desde un punto de vista inverso, las entidades más importantes son las sesiones por una parte y los contenidos por otra. Ambas entidades tienen agrupaciones superiores (grupos y perfiles), con el único objetivo de jerarquizar la estructura.

!!! warning "Importante"
    En este punto sólo se ha definido qué sesiones hay y qué contenidos existen, pero no sabemos qué relación hay entre sesiones y contenidos. Eso es responsabilidad del apartado de sesiones del catálogo de productos.

--8<-- "includes/SessionResultExamples.md"
=== "Sessions"

    ``` json
    {
        "SessionsGroupProfiles": [
            {
                "SessionsGroupProfileId": "cwj3q99xa8ara",
                "SessionsGroupProfileName": "Perfil de grupos por defecto",
                "SessionsGroups": [
                    {
                        "SessionsGroupId": "7q59grjg1tuxw",
                        "SessionsGroupName": "Sesiones de mañana",
                        "Sessions": [
                            {
                                "SessionId": "5b8qkqnmhdmk1",
                                "SessionTime": "2017-06-21T10:00:00",
                                "AvailableCapacity": 165
                            },
                            {
                                "SessionId": "5o3bwhx1ze1m1",
                                "SessionTime": "2017-09-06T10:00:00",
                                "AvailableCapacity": 230
                            }
                        ]
                    },
                    {
                        "SessionsGroupId": "gg5dfgrg1t12w",
                        "SessionsGroupName": "Sesiones de tarde",
                        "Sessions": [
                            {
                                "SessionId": "8qkqhdmknm5b1",
                                "SessionTime": "2017-06-21T17:00:00",
                                "AvailableCapacity": 165
                            },
                            {
                                "SessionId": "5hx1z3bowe1m1",
                                "SessionTime": "2017-09-06T17:00:00",
                                "AvailableCapacity": 230
                            }
                        ]
                    }
                ]
            }
        ],
        "SessionContentProfiles": [
            {
                "SessionContentProfileId": "5e8f65nherwpc",
                "SessionContentProfileName": "Perfil de contenidos por defecto",
                "SessionContents": [
                    {
                        "SessionContentId": "fiajih99h79ak",
                        "SessionContentName": "Película 1"
                    },
                    {
                        "SessionContentId": "m6noaxhzr33an",
                        "SessionContentName": "Película 2"
                    },
                    {
                        "SessionContentId": "suefs1zzn5ser",
                        "SessionContentName": "Película 3"
                    }
                ]
            }
        ],
        "Success": true,
        "Timestamp": "2022-02-18T17:02:27.8165916"
    }
    ```
