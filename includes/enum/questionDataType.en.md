The `DataType` determines which property the answer to the question must be sent in.

| `DataType` | Type | Answer property |
| ---: | --- | --- |
| 0 | Text | `StringValue` |
| 1 | List of texts | `StringCollectionValue` |
| 2 | Boolean | `BooleanValue` |
| 3 | List of booleans | `BooleanCollectionValue` |
| 4 | Date | `DateTimeValue` |
| 5 | List of dates | `DateTimeCollectionValue` |
| 6 | Integer number | `IntegerValue` |
| 7 | List of integers | `IntegerCollectionValue` |
| 8 | Decimal number | `DecimalValue` |
| 9 | List of decimals | `DecimalCollectionValue` |
| 10 | Select one value from a predefined set (`Values`) | `StringValue` |
| 11 | Select multiple values from a predefined set (`Values`) | `StringCollectionValue` |
| 12 | File | `BinaryValue` (+ `BinaryMimeType`, `BinaryExtension`) |
| 13 | List of files | `BinaryCollectionValue` (+ `BinaryMimeType`, `BinaryExtension`) |
