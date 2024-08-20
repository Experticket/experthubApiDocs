# Comprobar seguro de reembolso

Mediante este método podemos comprobar las pólizas de seguro de reembolso uno o varios productos, para una o múltiples fechas de acceso, precios.

!!! success ""
    Si el producto no tiene el campo **`IsInsurable`** del [catálogo](catalog.md) definido a `#!csharp true` entonces no es necesario realizar esta llamada.

!!! warning ""
    Si el producto tiene el campo **`IsInsurable`** del [catálogo](catalog.md) definido a `#!csharp true` entonces debemos realizar esta llamada cada vez que queramos ofrecer al cliente dicho producto para conocer si tiene la posibilidad de contratar un seguro de reembolso.

!!! info "¿Por qué hablamos de pólizas de seguro de reembolsos?"

    A nivel de producto, categoría y/o proveedor existe la posibilidad de contratar una póliza de seguro de reembolso para una venta.

## Método de acceso

**POST** /activity/InsurancePoliciesCheck

## Estructura de la petición

- **`LanguageCode`**: (``string``). Define el idioma en que se mostrarán los textos. *Formato ISO 639-1*.
- **`Sale`**: (``list``). Array de productos combinados.    
    - **`Products`**: (``list``). Array de productos incluidos en el producto combinado.
        - **`Id`**: (``string``). Identificador del cliente. Este se devolverá en la respuesta.
        - **`ProductId`**: (``string``). Identificador del producto combinado.
        - **`AccessDate`**: (``date``). Fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
        - **`Price`**: (``decimal``). Precio del producto para esa fecha.

### Ejemplos de petición

--8<-- "includes/examples/activity/checkInsurancePoliciesQueryExamples.md"

## Estructura de la respuesta

- **`InsurancePolicies`**: (``list``). Array de pólizas de seguro de reembolso.
    - **`Id`**: (``string``). Identificador de póliza.
    - **`Name`**: (``string``). Nombre de póliza.    
    - **`Quote`**: (``decimal``). Impuesto de la póliza.
    - **`CoverageAmount`**: (``decimal``). Cantidad de la cobertura de la póliza.
    - **`Sale`**: (``list``). Array de productos combinados.    
        - **`Products`**: (``list``). Array de productos incluidos en el producto combinado.
            - **`Id`**: (``string``). Identificador del cliente. Este se devolverá en la respuesta.
            - **`ProductId`**: (``string``). Identificador del producto combinado.
            - **`AccessDate`**: (``date``). Fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
            - **`Price`**: (``decimal``). Precio del producto para esa fecha.    
            - **`CoverageAmount`**: (``decimal``). Cantidad que cubre el seguro de reembolso.    
            - **`IsCovered`**: (``boolean``). Indica si está cubierto por el seguro de reembolso.    
    --8<-- "includes/responseBaseDocumentation.es.md"


### Ejemplos de respuesta

--8<-- "includes/examples/activity/checkInsurancePoliciesResponseExamples.md"
