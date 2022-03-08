# Reglas de flujo de venta

Las reglas de flujo de venta sirven para que se modifiquen o añadan productos automáticamente a la venta según una serie de condiciones que se cumplen dependiendo de los productos seleccionados.

??? info "Ejemplos"
    - Si se añaden cuatro unidades del producto 'Producto1' a la venta, se añade automáticamente una quinta unidad del producto a coste cero.
    - Si se añade el producto 'Product2' y además se añade el producto 'Producto3', se aplicará un 50% de descuento al producto 'Producto3'.
    - Por cada 20 niños añadidos a un grupo escolar, se añade una entrada de maestro gratis.

!!! tip "Importante"
    Las reglas no son acumulativas para un mismo producto. Si ya se ha aplicado una regla a un producto, este queda descartado para las siguientes reglas. El orden de aplicación de las reglas lo marca el campo ``Order`` del nodo ``Rules``.

## Método de acceso

**GET** activity/saleflowrules

## Estructura de la respuesta

- **``Rules``**: array de reglas.
    - **``Id``**: identificador de la regla.
    - **``Name``**: nombre de la regla.
    - **``Order``**: prioridad de la regla. Este campo indica el orden en que se aplicarán las reglas, ya que no se puede aplicar más de una regla a un mismo producto.
    - **``Inputs``**: array de productos a los que se aplican las reglas.
        - **``ProductId``**: identificador de producto.
    - **``Processors``**: array de procesadores que se encarga de aplicar las condiciones para los productos del campo ``Inputs``.
        - **``Value``**: cantidad de productos que se deben añadir a la venta para que se aplique este procesador.
        - **``OutputIfExistsApplicability``**: valor que indica como se procesarán las salidas producidas por este procesador.

            ??? example "Posibles valores"
                - 0: sin definir.
                - 1: el primero por orden.
                - 2: el más barato.
                - 3: el más caro.
                - 4: todos.

        - **``Outputs``**: son las salidas que produce la aplicación de procesador.
            - **``ProductId``**: identificador de producto que produce esta salida.
            - **``Order``**: prioridad de la salida. Se aplica si hay varias salidas y el valor del campo ``OutputIfExistsApplicability`` del procesador es igual a 1.
            - **``Quantity``**: cantidad de productos que produce esta salida.
            - **``ApplicationType``**: indica si esta salida se refiere a un producto que ya existía en la compra o se ha añadido uno nuevo.

                ??? example "Posibles valores"
                    - 1: se añade un nuevo producto a la salida.
                    - 2: se actualiza un producto que ya existe en ``Inputs``.

            - **``PriceModifierType``**: indica qué modificador de precio se aplica al producto.

                ??? example "Posibles valores"
                    - 1: porcentaje de descuento.
                    - 2: porcentaje de incremento.
                    - 3: descuento en valor absoluto.
                    - 4: incremento en valor absoluto.
                    - 5: precio total.

            - **``PriceModifierValue``**: indica qué valor de precio se aplica al producto.

- **``Success``**: booleano (`#!csharp true/false`) que indica si la petición se ha procesado correctamente.
- **``Timestamp``**: instante de tiempo del momento en que se procesa la petición. *Formato ISO 8601 (yyyy-MM-ddThh:mm:ss.fffffff)*.
- **``ErrorMessage``**: en caso de error incluye una breve descripción del problema.

### Ejemplo de respuesta

!!! info ""
    En el siguiente ejemplo podemos ver dos reglas:

    - **Regla descuento**: si la compra contiene los productos "twy5yhbishk91" y "uspeg7nr5st96" se actualiza el producto "twy5yhbishk91" con 5€ de descuento.
    - **Regla producto gratis (3x2)**: si la compra contiene el producto "hwuk9huaqopwo" con cantidad 2, se añade el producto "twy5yhbishk91" con un 100% de descuento.

--8<-- "includes/examples/activity/saleFlowRulesResponseExamples.md"
