# Prepaquetes

Con este método podemos obtener los prepaquetes de actividades disponibles.

Los prepaquetes son estructuras previas a la creación de un paquete y pueden estar compuestos por uno o más recintos (ej. "Oceanogràfic + Bioparc"). Cada prepaquete, a su vez, dispondrá de uno o varios grupos de productos (ProductPaxGroupings).

Es relevante tener en cuenta la geolocalización sugerida. Esta se utiliza en los distintos métodos de catálogo para ubicar una zona a partir de la cual buscar hoteles.

## Método de acceso

**POST** activity/prepackages

## Estructura de la petición
Todos los parámetros de la petición son opcionales.

- **``ProviderIds``**: array de proveedores para filtrar.
- **``PrePackageIds``**: array de prepaquetes para filtrar.
- **``FromDate``**: fecha desde para filtrar prepaquetes. Por defecto se coge el día actual. *Formato ISO 8601 (yyyy-MM-dd)*.
- **``ToDate``**: fecha hasta para filtrar prepaquetes. Por defecto será la fecha dentro de un año. *Formato ISO 8601 (yyyy-MM-dd)*.
- **``PeopleDistributions``**: tipo de personas para filtrar prepaquetes.
    - **``NumberOfAdults``**: número de adultos.
    - **``NumberOfChildren``**: número de niños.
    - **``NumberOfSeniors``**: número de seniors.
    - **``NumberOfBabies``**: número de bebés.
    - **``ChildrenAges``**: array de edades de niños y bebés.

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
