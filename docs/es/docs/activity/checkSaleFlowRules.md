# Comprobar reglas de flujo de venta

Antes de hacer una compra podemos comprobar si se va a aplicar alguna de las reglas que hemos visto en [Reglas de flujo de venta](saleFlowRules.md) sin que tenga ningúna consecuencia a efectos prácticos.

Una vez lanzada la consulta se devolverá, a modo informativo, los datos suficientes para saber cómo quedaría la compra en caso de finalizarse.

## Método de acceso

**POST** activity/saleflowrules

## Estructura de la petición

- **``ApiKey``**: clave única y privada que identifica al colaborador. *La ApiKey se obtendrá desde el AdminPartner*.
- **``AccessDateTime``**: fecha de acceso. *Formato ISO 8601 (yyyy-MM-dd)*.
- **``Products``**: productos que componen la venta.
    - **``AccessDateTime``**: *opcional*, fecha de acceso. Si se define a nivel de producto tiene precedencia sobre la fecha definida a nivel global.
    - **``ProductId``**: identificador del producto. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **``Quantity``**: *opcional*, cantidad. Por defecto su valor es 1.

### Ejemplo de petición

!!! info "Ejemplo 1: regla producto gratis (3x2)"
    En este ejemplo vamos a elegir 4 productos "hwuk9huaqopwo". Por lo tanto en los datos de salida deberemos ver aplicada la regla "Regla producto gratis 3x2" vista en los [ejemplos Reglas de flujo de venta](saleFlowRules.md#ejemplo-de-respuesta). Es decir, como pedimos 4 productos "hwuk9huaqopwo" debemos obtener gratis otros dos productos "twy5yhbishk91".
!!! info "Ejemplo 2: regla producto con descuento y fecha de acceso diferente (Discount)"
    En este ejemplo vamos a elegir un producto "twy5yhbishk91" y un producto "uspeg7nr5st96" con una fecha de acceso diferente. Por lo tanto en los datos de salida deberemos ver aplicada la regla "Regla descuento" vista en los [ejemplos Reglas de flujo de venta](saleFlowRules.md#ejemplo-de-respuesta). Es decir, veremos 5€ de descuento en el producto "twy5yhbishk91".

--8<-- "includes/examples/activity/checkSaleFlowRulesQueryExamples.md"

## Estructura de la respuesta

- **``NotModifiedProducts``**: array que contiene productos que no han sido modificados.
    - **``ProductId``**: identificador del producto.
    - **``AccessDateTime``**: fecha de acceso del producto. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **``OriginalPrice``**: precio sin modificar del producto.
    - **``Price``**: precio final producto.
- **``ModifiedProducts``**: array que contiene productos modificados que ya estaban incluidos en la venta.
    - **``ProductId``**: identificador del producto.
    - **``AccessDateTime``**: fecha de acceso del producto. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **``OriginalPrice``**: precio sin modificar del producto.
    - **``Price``**: precio final producto.
    - **``SaleFlowRuleId``**: identificador de la regla.
    - **``SaleFlowRuleCommercialName``**: nombre descriptivo que se da a la regla para poder mostrar al usuario.
    - **``SaleFlowRuleDescripción``**: descripción de la regla aplicada.
    - **``SaleFlowRuleName``**: nombre de la regla aplicada.
- **``AddedProducts``**: array que contiene productos añadidos que no estaban incluidos en la venta.
    - **``ProductId``**: identificador del producto.
    - **``AccessDateTime``**: fecha de acceso del producto. *Formato ISO 8601 (yyyy-MM-dd)*.
    - **``OriginalPrice``**: precio sin modificar del producto.
    - **``Price``**: precio final producto.
    - **``SaleFlowRuleId``**: identificador de la regla.
    - **``SaleFlowRuleCommercialName``**: nombre descriptivo que se da a la regla para poder mostrar al usuario.
    - **``SaleFlowRuleDescripción``**: descripción de la regla aplicada.
    - **``SaleFlowRuleName``**: nombre de la regla aplicada.
- **``Success``**: booleano (``#!csharp true/false``) que indica si la petición se ha procesado correctamente.
- **``Timestamp``**: instante de tiempo en el que se procesa la petición. *Formato ISO 8601 (yyyy-MM-ddThh:mm:ss.fffffff)*.
- **``ErrorMessage``**: en caso de error contiene una breve descripción del problema.

### Ejemplo de respuesta

--8<-- "includes/examples/activity/checkSaleFlowRulesResponseExamples.md"
