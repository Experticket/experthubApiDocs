# Sesiones

Una sesión está definida por una fecha y hora, un contenido y, opcionalmente, el aforo disponible.

Según esta definición, se entiende que una misma sesión puede ser compartida por varios tickets. Los tickets "Entrada adulto", "Entrada niño", "Entrada junior", "Entrada senior" y "Entrada discapacitado" pueden tener asociadas las mismas sesiones durante el año en curso (por ejemplo, 10 sesiones al día durante los 365 días del año).

Como esta casuística puede ser habitual, se ha procurado separar lo máximo posible la estructura de sesiones del catálogo de productos. Siguiendo con el ejemplo anterior, si se definiesen las sesiones en el catálogo de productos tendríamos 10 sesiones x 365 días = 3650 sesiones para cada uno de los 5 tickets ("Entrada adulto, "Entrada niño", "Entrada junior", "Entrada senior" y "Entrada discapacitado").

Por lo tanto, se define la estructura de sesiones, para minimizar la carga de datos y jerarquizar lo mejor posible el catálogo de sesiones.

## Método de acceso

**POST** actvity/sessions

## Estructura de la petición

Para obtener las sesiones podemos utilizar diferentes filtros en el cuerpo del método. Cada filtro se considerará un ***AND***.

- **`SessionsGroupProfileIds`**: array de perfiles de grupos de sesión.
- **`SessionsGroupIds`**: array de grupos de sesión.
- **`SessionContentProfileIds`**: array de perfiles de contenido de sesión.
- **`FromDate`**: filtrado por fecha de inicio. No permite valores menores al día de hoy. El valor por defecto es el día actual. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`ToDate`**: filtrado por fecha de fin. Su valor por defecto es la fecha correnpondiente a dentro de un año. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`Dates`**: array de fechas por las que filtrar. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`LanguageCode`**: código del idioma de los contenidos.

### Ejemplos de petición

--8<-- "includes/examples/activity/sessionsQueryExamples.md"

## Estructura de la respuesta

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
            - **`AvailableCapacity`**: valor que indica el aforo de la sesión. Si este campo no existe, es que no hay un aforo limitado. Si sólo se quiere consultar el aforo de una sesión, se puede utilizar el método descrito en [Obtención del aforo disponible](availability.md).
- **`SessionContentProfiles`**: array de perfiles de contenidos de sesión.
    - **`SessionContentProfileId`**: identificador del perfil de contenidos de sesión.
    - **`SessionContentProfileName`**: nombre del perfil de contenidos de sesión.
    - **`SessionContents`**: array de contenidos de sesión.
        - **`SessionContentId`**: identificador del contenido de sesión.
        - **`SessionContentName`**: nombre del contenido de sesión.
        - **`SessionContentDescription`**: descripción del contenido de sesión.
--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

Como ejemplo, supongamos que tenemos un perfil de grupos de sesión por defecto y un perfil de contenidos de sesión por defecto.

Dentro del perfil de grupos de sesión vemos que tenemos dos grupos de sesión:

- Sesiones de mañana, que agrupa las sesiones de las 10:00h de la mañana.
- Sesiones de tarde, que agrupa las sesiones de las 17:00h de la tarde.

En el perfil de contenidos de sesión tenemos tres contenidos de sesión, que definen películas (la 1, la 2 y la 3).

Observado desde un punto de vista inverso, las entidades más importantes son las sesiones por una parte y los contenidos por otra. Ambas entidades tienen agrupaciones superiores (grupos y perfiles), con el único objetivo de jerarquizar la estructura.

!!! warning "Importante"
    En este punto sólo se ha definido qué sesiones hay y qué contenidos existen, pero no sabemos qué relación hay entre sesiones y contenidos. Eso es responsabilidad del apartado de sesiones del catálogo de productos.

--8<-- "includes/examples/activity/sessionResultExamples.md"
