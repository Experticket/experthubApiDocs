# Comprobar reglas de flujo de venta

Antes de hacer una compra podemos comprobar si se va a aplicar alguna de las reglas que hemos visto en [Reglas de flujo de venta](saleFlowRules.md) sin que tenga ninguna consecuencia a efectos prácticos.

Una vez lanzada la consulta se devolverá, a modo informativo, los datos suficientes para saber cómo quedaría la compra en caso de finalizarse.

## Método de acceso

**POST** activity/saleflowrules

## Estructura de la petición

- **``AccessDateTime``**: (``date``). Fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
- **``Products``**: (``list``). Productos que componen la venta.
    - **``AccessDateTime``**: (``date``) ``Opcional``. Fecha de acceso. Si se define a nivel de producto tiene precedencia sobre la fecha definida a nivel global. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **``ProductId``**: (``string``). Identificador del producto.
    - **``Quantity``**: (``int``) ``Opcional``. Cantidad. Por defecto su valor es 1.
- **``DynamicProviders``**: (``list``). Proveedores dinámicos que componen la venta.
    - **``AccessDateTime``**: (``date``) ``Opcional``. Fecha de acceso. Si se define a nivel de producto tiene precedencia sobre la fecha definida a nivel global. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **``ProviderId``**: (``string``). Identificador del proveedor dinámico.
    - **``Quantity``**: (``int``) ``Opcional``. Cantidad. Por defecto su valor es 1.
- **`LanguageCode`**: (``string``) ``Opcional``. Define el idioma en que se mostrarán los textos. Por defecto se devolverá el idioma configurado para el colaborador. *Formato ISO 639-1*.

### Ejemplo de petición

!!! info "Ejemplo 1: regla producto gratis (3x2)"
    En este ejemplo vamos a elegir 4 productos "hwuk9huaqopwo". Por lo tanto en los datos de salida deberemos ver aplicada la regla "Regla producto gratis 3x2" vista en los [ejemplos Reglas de flujo de venta](saleFlowRules.md#ejemplo-de-respuesta). Es decir, como pedimos 4 productos "hwuk9huaqopwo" debemos obtener gratis otros dos productos "twy5yhbishk91".
!!! info "Ejemplo 2: regla producto con descuento y fecha de acceso diferente (Discount)"
    En este ejemplo vamos a elegir un producto "twy5yhbishk91" y un producto "uspeg7nr5st96" con una fecha de acceso diferente. Por lo tanto en los datos de salida deberemos ver aplicada la regla "Regla descuento" vista en los [ejemplos Reglas de flujo de venta](saleFlowRules.md#ejemplo-de-respuesta). Es decir, veremos 5€ de descuento en el producto "twy5yhbishk91".

--8<-- "includes/examples/activity/checkSaleFlowRulesQueryExamples.md"

## Estructura de la respuesta

- **``NotModifiedProducts``**: (``list``). Array que contiene productos que no han sido modificados.
    - **``ProductId``**: (``string``). Identificador del producto.
    - **``AccessDateTime``**: (``date``). Fecha de acceso del producto. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **``OriginalPrice``**: (``decimal``). Precio sin modificar del producto.
    - **``Price``**: (``decimal``). Precio final producto.
- **``ModifiedProducts``**: (``list``). Array que contiene productos modificados que ya estaban incluidos en la venta.
    - **``ProductId``**: (``string``). Identificador del producto.
    - **``AccessDateTime``**: (``date``). Fecha de acceso del producto. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **``OriginalPrice``**: (``decimal``). Precio sin modificar del producto.
    - **``Price``**: (``decimal``). Precio final producto.
    - **``SaleFlowRuleId``**: (``string``). Identificador de la regla.
    - **``SaleFlowRuleCommercialName``**: (``string``). Nombre descriptivo que se da a la regla para poder mostrar al usuario.
    - **``SaleFlowRuleDescripción``**: (``string``). Descripción de la regla aplicada.
    - **``SaleFlowRuleName``**: (``string``). Nombre de la regla aplicada.
- **``AddedProducts``**: (``list``). Array que contiene productos añadidos que no estaban incluidos en la venta.
    - **``ProductId``**: (``string``). Identificador del producto.
    - **``AccessDateTime``**: (``date``). Fecha de acceso del producto. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **``OriginalPrice``**: (``decimal``). Precio sin modificar del producto.
    - **``Price``**: (``decimal``). Precio final producto.
    - **``SaleFlowRuleId``**: (``string``). Identificador de la regla.
    - **``SaleFlowRuleCommercialName``**: (``string``). Nombre descriptivo que se da a la regla para poder mostrar al usuario.
    - **``SaleFlowRuleDescripción``**: (``string``). Descripción de la regla aplicada.
    - **``SaleFlowRuleName``**: (``string``). Nombre de la regla aplicada.
--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/checkSaleFlowRulesResponseExamples.md"
