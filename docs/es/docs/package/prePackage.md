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

### Ejemplo de petición

--8<-- "includes/examples/package/prepackageQueryExamples.md"

## Estructura de la respuesta

- **``PrePackages``**: array de prepaquetes.
    - **``Id``**: identificador del prepaquete.
    - **``Order``**: orden para ser mostrados.
    - **``Image``**: imagen promocional del prepaquete.
    - **``Description``**: descripción del prepaquete.
    - **``Name``**: nombre del prepaquete.
    - **``CommercialName``**: nombre comercial del prepaquete.
    - **``ProductPaxGroupings``**: agrupación de productos.
        - **``ProviderId``**: identificador del proveedor.
        - **``ProviderName``**: nombre del proveedor.
        - **``ProviderLocation``**: localización del proveedor.
            - **`Lat`**: coordenadas de latitud.
            - **`Lng`**: coordenadas de longitud.
        - **``DatePolicyKey``**: clave de políticas de fecha.
        - **``TicketEnclosures``**: array de recintos.
            - **``Id``**: identificador del recinto.
            - **``Name``**: nombre del recinto.
            - **``Logo``**: imagen con el logotipo del recinto.
        - **``ValidDays``**: días de validez.
        - **``ValidDaysType``**: tipo de días de validez.
    - **``SuggestedLocation``**: localización sugerida para búsqueda de alojamiento. Suele ser unas coordenadas calculadas céntricas entre todos los recintos del prepaquete.
        - **`Lat`**: coordenadas de latitud.
        - **`Lng`**: coordenadas de longitud.
--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/package/prepackageResponseExamples.md"
