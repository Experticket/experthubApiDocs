# Cotizar pólizas de seguro

Mediante este método podemos comprobar las pólizas de seguro de reembolso para uno o varios productos y una o múltiples fechas de acceso.

!!! success ""
    Si en los PartnerSettings del [catálogo](catalog.md) no está definido a `#!csharp true` el parámetro **`IsInsurancePolicyEnabled`** o el proveedor/categoría/producto NO tiene el campo **`IsInsurable`** del [catálogo](catalog.md) definido a `#!csharp true`~~~~entonces no es necesario realizar esta llamada.

!!! warning ""
    Si el proveedor/categoría/producto tiene el campo **`IsInsurable`** del [catálogo](catalog.md) definido a `#!csharp true` entonces debemos realizar esta llamada cada vez que queramos ofrecer al cliente dicho la posibilidad de contratar un seguro de reembolso de 1 o N productos.

!!! info "¿Por qué hablamos de pólizas de seguro de reembolsos?"

    Cuando vamos a finalizar la venta existe la posibilidad de contratar una póliza de seguro de reembolso de 1 o N productos que componen la venta.

## Método de acceso

**POST** /activity/InsurancePolicyCheck 

## Estructura de la petición

- **`LanguageCode`**: (``string``). Define el idioma en que se mostrarán los textos. *Formato ISO 639-1*.
- **`Sale`**: (``object``). Datos de la venta. Es importante destacar que DEBEN enviarse TODOS los elementos que componen la venta (no solo los de los productos asegurables), exceptuando los añadidos por [reglas de flujo de venta](checkSaleFlowRules.md)
    - **`Products`**: (``list``). Array de todos los productos que componen la venta. NO deben incluirse los productos combinados.
        - **`Id`**: (``string``). Identificador único que servirá como identificador espejo, es decir que se devolverá en los datos de la respuesta.
        - **`ProductId`**: (``string``). Identificador del producto.
        - **`AccessDate`**: (``date``). Fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **`CombinedProducts`**: (``list``). Array de productos combinados.
        - **`Id`**: (``string``). Identificador único que servirá como identificador espejo, es decir que se devolverá en los datos de la respuesta.
        - **`CombinedProductId`**: (``string``). Identificador del producto combinado.
        - **`Products`**: (``list``). Array de productos que componen el producto combinado (con la misma estructura que el listado de productos que componen la venta).
    - **`Packages`**: (``list``). Array de paquetes.
        - **`EchoToken`**: (``string``). Token que identifica a la secuencia de peticiones. Ver [catálogo extendido](../fullCatalog#estructura-de-la-respuesta)
        - **`PackageId`**: (``string``). Identificador del paquete.
        - **`Activities`**: (``list``). Actividades que componen el paquete
            - **`Id`**: (``string``). Identificador único que servirá como identificador espejo, es decir que se devolverá en los datos de la respuesta.
            - **`ProductId`**: (``string``). Identificador del producto.
            - **`AccessDate`**: (``date``). Fecha de acceso. Formato ISO 8601 (YYYY-MM-DD).
    - **`Accommodations`**: (``list``). Array de alojamientos.
        -  **`EchoToken`**: (``string``). Token que identifica a la secuencia de peticiones. Ver [catálogo extendido](../fullCatalog#estructura-de-la-respuesta)
        -  **`RateId`**: (``string``). Identificador de la tarifa~~~~
- **`DiscountCouponCodes`**: (``object``). Array de códigos de cupones descuento que forman parte de la venta. Esta información es necesaria para conformar el precio final a cotizar de la póliza.

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
