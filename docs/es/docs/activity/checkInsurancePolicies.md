# Comprobar seguro de reembolso

Mediante este método podemos comprobar las pólizas de seguro de reembolso para uno o varios productos, una o múltiples fechas de acceso y diferentes precios.

!!! success ""
    Si el  proveedor/categoría/producto NO tiene el campo **`IsInsurable`** del [catálogo](catalog.md) definido a `#!csharp true` entonces no es necesario realizar esta llamada.

!!! warning ""
    Si el proveedor/categoría/producto tiene el campo **`IsInsurable`** del [catálogo](catalog.md) definido a `#!csharp true` entonces debemos realizar esta llamada cada vez que queramos ofrecer al cliente dicho la posibilidad de contratar un seguro de reembolso de 1 o N productos.

!!! info "¿Por qué hablamos de pólizas de seguro de reembolsos?"

    Cuando vamos a finalizar la venta existe la posibilidad de contratar una póliza de seguro de reembolso de 1 o N productos que componen la venta.

## Método de acceso

**POST** /activity/InsurancePoliciesCheck

## Estructura de la petición

- **`LanguageCode`**: (``string``). Define el idioma en que se mostrarán los textos. *Formato ISO 639-1*.
- **`Sale`**: (``object``). Datos de la venta.    
    - **`Products`**: (``list``). Array de productos sobre los que se quieren consultar las pólizas de seguros.
        - **`Id`**: (``string``). Identificador del cliente. Este se devolverá en la respuesta.
        - **`ProductId`**: (``string``). Identificador del producto.
        - **`AccessDate`**: (``date``). Fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
        - **`Price`**: (``decimal``). Precio del producto para esa fecha.

### Ejemplos de petición

--8<-- "includes/examples/activity/checkInsurancePoliciesQueryExamples.md"

## Estructura de la respuesta

- **`InsurancePolicies`**: (``list``). Array de pólizas de seguro de reembolso.
    - **`Id`**: (``string``). Identificador de póliza.
    - **`Name`**: (``string``). Nombre de póliza.    
    - **`Quote`**: (``decimal``). Valor de cotización de la póliza, es decir, el precio que le cuesta la póliza al cliente.
    - **`CoverageAmount`**: (``decimal``). Cantidad de la cobertura de la póliza.
    - **`Sale`**: (``object``). Información de la venta.    
        - **`Products`**: (``list``). Array de productos incluidos.
            - **`Id`**: (``string``). Identificador del cliente. Este se devolverá en la respuesta.
            - **`ProductId`**: (``string``). Identificador del producto.
            - **`AccessDate`**: (``date``). Fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
            - **`Price`**: (``decimal``). Precio del producto para esa fecha.    
            - **`CoverageAmount`**: (``decimal``). Cantidad que cubre el seguro de reembolso.    
            - **`IsCovered`**: (``boolean``). Indica si está cubierto por el seguro de reembolso.    
    --8<-- "includes/responseBaseDocumentation.es.md"


### Ejemplos de respuesta

--8<-- "includes/examples/activity/checkInsurancePoliciesResponseExamples.md"
