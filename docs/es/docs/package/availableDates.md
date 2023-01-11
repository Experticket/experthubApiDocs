# Disponibilidad de fechas

Este método nos permite obtener la disponibildiad de fechas para un packete específico.

## Método de acceso

**POST** /Package/AvailableDates

## Estructura de la petición

- **``EchoToken``**: (``string``). Token que identifica a la secuencia de peticiones. Ver [catálogo extendido](../extendedCatalog#estructura-de-la-respuesta)
- **``PackageId``**: (``string``). Identificador del paquete. Ver la propiedad ``Packages.Package.Id`` de [catálogo extendido](../extendedCatalog#estructura-de-la-respuesta)

### Ejemplos

??? tip "Example"
    --8<-- "includes/examples/package/availableDates.request.1.md"

## Estructura de la respuesta

### Ejemplos
