# Disponibilidad de fechas

Este método nos permite obtener la disponibildiad de fechas para cada actividad disponible dentro del paquete solicitado. 

??? important "Implicaciones"

    Teniendo en cuenta que un paquete puede estar compuesto por una o más actividades, es posible que exista alguna restricción de acceso y no se puedan relizar todas las actividades el mismo día. Esto podría deberse a la distancia entre ellas, por el tiempo requerido para hacer cada una de esas actividades o por cualquier otra restricción/incompatibildiad que se haya creado.

    Por lo tanto, deberemos llamar a este método tantas veces como actividades compongan el paquete solicitado.

    En la primera llamada indicaremos el identificador de paquete (``PackageId``) y omitiremos las agrupaciones por fechas (``PaxGroupingsDates``). La respuesta mostrará un listado con la disponibilidad de las distintas actividades que compongan el paquete. De esta forma, el cliente, podrá seleccionar la fecha de acceso de la **primera** actividad. La primera actividad puede ser cualquier actividad de las mostradas en la respuesta.

    Una vez tengamos la información de la primera actividad y la fecha elegida por el cliente, llamaremos nuevamente a este método añadiendo, en ``PaxGroupingsDates``, esta elección. La respuesta mostrará un listado con la disponibilidad de las **siguientes** actividades que compongan el paquete, teniendo en cuenta las **posibles** restricciones y, de esta forma, permitir al cliente escoger esa segunda actividad y fecha de acceso.

    Iremos repitiendo esta última acción, con el resto de actividades.

    === "Ejemplo primera llamada"

        --8<-- "includes/examples/package/availableDates.request.1.md"

    === "Ejemplo segunda llamada"

        --8<-- "includes/examples/package/availableDates.request.2.md"
    
    === "Ejemplo tercera llamada y sucesivas"

        --8<-- "includes/examples/package/availableDates.request.3.md"


## Método de acceso

**POST** /Package/AvailableDates

## Estructura de la petición

- **``EchoToken``**: (``string``). ``Requerido``. Token que identifica a la secuencia de peticiones. Ver [catálogo extendido](../extendedCatalog#estructura-de-la-respuesta)
- **``PackageId``**: (``string``). ``Requerido``. Identificador del paquete. Ver la propiedad ``Packages.Package.Id`` de [catálogo extendido](../extendedCatalog#estructura-de-la-respuesta)
- **``PaxGroupingsDates``**: (``list``). ``Opcional``. Listado de agrupaciones y fechas ya seleccionadas.
    - **``PaxGroupingDates``**: (``object``). ``Opcional``. Información de la agrupación.
        - **``Id``**: (``string``). ``Requerido``. Identificador de la agrupación ``ProductPaxGroupingId``.
        - **``Date``**: (``date``). ``Requerido``. Fecha de acceso a la actividad.

### Ejemplos

??? tip "Example"
    
    --8<-- "includes/examples/package/availableDates.request.3.md"

## Estructura de la respuesta

- **``PaxGroupingsDates``**: (``list``). Listado de agrupaciones.
    - **``PaxGroupingDates``**: (``object``). Información de la agrupación.
        - **``Id``**: (``string``). Identificador de la agrupación (``PaxGroupingId``).
        - **``Dates``**: (``list``). Listado de fechas disponibles.
            - **``(date)``**: Fecha con disponibilidad. Formato IS0 8601 (YYYY-MM-DD). 

### Ejemplos

??? tip "Example"
    
    --8<-- "includes/examples/package/availableDates.response.1.md"