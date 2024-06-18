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

- **``Rules``**: (``list``). Array de reglas.
    - **``Id``**: (``string``). Identificador de la regla.
    - **``Name``**: (``string``). Nombre de la regla.
    - **``Order``**: (``byte``). Prioridad de la regla. Este campo indica el orden en que se aplicarán las reglas, ya que no se puede aplicar más de una regla a un mismo producto.
    - **``Inputs``**: (``lista``). Array de productos a los que se aplican las reglas.
        - **``ProductId``**: (``string``). Identificador de producto.
    - **``Processors``**: (``lista``). Array de procesadores que se encarga de aplicar las condiciones para los productos del campo ``Inputs``.
        - **``Value``**: (``byte``). cantidad de productos que se deben añadir a la venta para que se aplique este procesador.
        - **``OutputIfExistsApplicability``**: (``byte``). Valor que indica cómo se procesarán las salidas producidas por este procesador.

            ??? example "Posibles valores"
                - 0: sin definir.
                - 1: el primero por orden.
                - 2: el más barato.
                - 3: el más caro.
                - 4: todos.

        - **``Outputs``**: (``list``). Son las salidas que produce la aplicación de procesador.
            - **``ProductId``**: (``string``). Identificador de producto que produce esta salida.
            - **``Order``**: (``byte``). Prioridad de la salida. Se aplica si hay varias salidas y el valor del campo ``OutputIfExistsApplicability`` del procesador es igual a 1.
            - **``Quantity``**: (``byte``). Cantidad de productos que produce esta salida.
            - **``ApplicationType``**: (``byte``). Indica si esta salida se refiere a un producto que ya existía en la compra o se ha añadido uno nuevo.

                ??? example "Posibles valores"
                    - 1: se añade un nuevo producto a la salida.
                    - 2: se actualiza un producto que ya existe en ``Inputs``.

            - **``PriceModifierType``**: (``byte``). Indica qué modificador de precio se aplica al producto.

                ??? example "Posibles valores"
                    - 1: porcentaje de descuento.
                    - 2: porcentaje de incremento.
                    - 3: descuento en valor absoluto.
                    - 4: incremento en valor absoluto.
                    - 5: precio total.

            - **``PriceModifierValue``**: (``decimal``). Indica qué valor de precio se aplica al producto.

--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

!!! info ""
    En el siguiente ejemplo podemos ver dos reglas:

    - **Regla descuento**: si la compra contiene los productos "twy5yhbishk91" o "uspeg7nr5st96" se actualiza el producto "twy5yhbishk91" con 5€ de descuento.
    - **Regla producto gratis (3x2)**: si la compra contiene el producto "hwuk9huaqopwo" con cantidad 2, se añade el producto "twy5yhbishk91" con un 100% de descuento.

--8<-- "includes/examples/activity/saleFlowRulesResponseExamples.md"
