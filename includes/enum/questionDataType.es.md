El `DataType` determina en qué propiedad debe enviarse la respuesta de la pregunta.

| `DataType` | Tipo | Propiedad de respuesta |
| ---: | --- | --- |
| 0 | Texto | `StringValue` |
| 1 | Lista de textos | `StringCollectionValue` |
| 2 | Booleano | `BooleanValue` |
| 3 | Lista de booleanos | `BooleanCollectionValue` |
| 4 | Fecha | `DateTimeValue` |
| 5 | Lista de fechas | `DateTimeCollectionValue` |
| 6 | Número entero | `IntegerValue` |
| 7 | Lista de enteros | `IntegerCollectionValue` |
| 8 | Número decimal | `DecimalValue` |
| 9 | Lista de decimales | `DecimalCollectionValue` |
| 10 | Selección de un valor entre un conjunto predefinido (`Values`) | `StringValue` |
| 11 | Selección de varios valores entre un conjunto predefinido (`Values`) | `StringCollectionValue` |
| 12 | Archivo | `BinaryValue` (+ `BinaryMimeType`, `BinaryExtension`) |
| 13 | Lista de archivos | `BinaryCollectionValue` (+ `BinaryMimeType`, `BinaryExtension`) |
