# Prepaquetes

Con este método podemos obtener los prepaquetes de actividades disponibles.

Los prepaquetes son estructuras previas a la creación de un paquete y pueden estar compuestos por uno o más recintos (ej. "Oceanogràfic + Bioparc"). Cada prepaquete, a su vez, dispondrá de uno o varios grupos de productos (ProductPaxGroupings).

Es relevante tener en cuenta la geolocalización sugerida. Esta se utiliza en los distintos métodos de catálogo para ubicar una zona a partir de la cual buscar hoteles.

## Método de acceso

**POST** Activity/Prepackages

## Estructura de la petición
Todos los parámetros de la petición son opcionales.

- **``ProviderIds``**: (``list``) ``Opcional``. Listado de proveedores para filtrar.
    - **``(string)``**: ``Opcional``. Identificador del proveedor.
- **``PrePackageIds``**: (``list``) ``Opcional``. Listado de prepaquetes para filtrar.
    - **``(string)``**: ``Opcional``. Identificador del prepaquete.
- **``FromDate``**: (``date``) ``Opcional``. Fecha incial para filtrar prepaquetes. Valor por defecto: día actual. Formato IS0 8601 (YYYY-MM-DD).
- **``ToDate``**: (``date``) ``Opcional``. Fecha final para filtrar prepaquetes. Valor por defecto: un año a futuro. Formato IS0 8601 (YYYY-MM-DD).
- **``PeopleDistributions``**: (``list``) ``Opcional``. Listado con la distribución de personas en las distintas habitaciones.
    - **``PeopleDistribution``**: (``object``) ``Opcional``. Información de la distribución en la habitación correspondiente.
        - **``NumberOfAdults``**: (``int``) ``Opcional``. Número de adultos.
        - **``NumberOfChildren``**: (``int``) ``Opcional``. Número de niños.
        - **``NumberOfSeniors``**: (``int``) ``Opcional``. Número de seniors.
        - **``NumberOfBabies``**: (``int``) ``Opcional``. Número de bebés.
        - **``ChildrenAges``**: (``list``) ``Opcional``. Listado con las edades de los bebés y niños.
            - **``(int)``**: ``Opcional``. Edad del bebe o niño.

!!! caution "Edad de los bebés/niños"
    Se deberá preguntar la edad de todas aquellas personas que tengan 17 años o menos.

### Ejemplo de petición

--8<-- "includes/examples/package/prepackageQueryExamples.md"

## Estructura de la respuesta

- **`Success`**: (``boolean``). Indica si la llamada ha sido procesada satisfactoriamente.
- **`Timestamp`**: (``dateTime``). instante de tiempo en el que se procesó la petición. Formato ISO 8601 (yyyy-MM-ddThh\:mm\:ss.fffffff).
- **``PrePackages``**: (``list``). Listado de prepaquetes disponibles.
    - **``PrePackage``**: (``object``). Información del prepaquete.
        - **``Id``**: (``string``). Identificador del prepaquete.
        - **``Order``**: (``int``). Orden para ser mostrados.
        - **``Image``**: (``string``). Url de la imagen promocional del prepaquete.
        - **``Description``**: (``string``). Descripción del prepaquete.
        - **``Name``**: (``string``). Nombre del prepaquete.
        - **``CommercialName``**: (``string``). Nombre comercial del prepaquete.
        - **``ProductPaxGroupings``**: (``list``). Listado de agrupación de productos.
            - **``ProductPaxGrouping``**: (``object``). Información de la agrupación de productos.
                - **``ProviderId``**: (``string``). Identificador del proveedor.
                - **``ProviderName``**: (``string``). Nombre del proveedor.
                - **``ProviderLocation``**: (``string``). Localización del proveedor.
                    - **`Lat`**: (``decimal``). Coordenadas de latitud.
                    - **`Lng`**: (``string``). Coordenadas de longitud.
                - **``DatePolicyKey``**: (``int``). Clave de políticas de fecha. Todos los productos con la misma clave, deberán compartir fecha de acceso.
                - **``TicketEnclosures``**: (``list``). Listado de recintos.
                    - **``TicketEnclosure``**: (``object``). Información del recinto.
                        - **``Id``**: (``string``). Identificador del recinto.
                        - **``Name``**: (``string``). Nombre del recinto.
                        - **``Logo``**: (``string``). Url de la imagen con el logotipo del recinto.
                - **``ValidDays``**: (``int``). Días de validez.
                - **``ValidDaysType``**: (``int``). Tipo de días de validez.
                    
                    ??? example "Posibles valores"
                        --8<-- "includes/enum/validDayType.md"

                - **``ProductPaxGroupingId``**: (``string``). Identificador del producto agrupado.
                - **``ProductPaxGroupingName``**: (``string``). Nombre del producto agrupado.

            - **``SuggestedLocation``**: (``object``). Localización sugerida para búsqueda de alojamiento. Suele ser unas coordenadas calculadas céntricas entre todos los recintos del prepaquete.
                - **`Lat`**: (``decimal``). Coordenadas de latitud.
                - **`Lng`**: (``decimal``). Coordenadas de longitud.

### Ejemplo de respuesta

--8<-- "includes/examples/package/prepackageResponseExamples.md"
