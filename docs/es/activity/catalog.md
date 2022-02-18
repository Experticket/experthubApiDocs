# Obtención del catálogo de actividades

En un primer paso, tendrá que obtener todo el catálogo completo de proveedores, categorías (productBases) y productos para su tratamiento interno.

La información del catálogo incluye los identificadores únicos de Proveedor, Producto y Ticket que posteriormente se usarán para añadir cualquier producto al carrito.

También incluirá otros datos como el precio de los productos dependiendo de las fechas, o las condiciones comerciales del producto.

Siguiendo con nuestro ejemplo, podría darse el caso de que el producto "Entrada 2x1 Niño" del proveedor PAC baje el precio y aumente el periodo de validez de la venta.

## Método de acceso

**POST** /activity/catalog

## Estructura de datos de envío

Para obtener el catálogo podemos utilizar diferentes filtros en el body del método.

Cada filtro se considerará un ***AND***. Por ejemplo, pueden filtrarse por varios *ProductIds* pero no tiene sentido filtrar por *ProviderIds* y por *ProductIds* siendo este último de un proveedor diferente.

- **`ProviderIds`**: `#!csharp List<string>` lista identificadores de proveedor.
- **`ProductBaseIds`**: `#!csharp List<string>` lista identificadores de categoría.
- **`ProductIds`**: `#!csharp List<string>` lista identificadores de producto.
- **`FromDate`**: `#!csharp string` fecha de inicio. No permite valores menores al día actual. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`ToDate`**: `#!csharp string` fecha de fin. Por defecto su valor es el de la fecha correspondiente a dentro de un año. *Formato ISO 8601 (yyyy-MM-dd)*.
- **`ReferenceDate`**: `#!csharp string` exige que el día que se tome como referencia para el cálculo de precios y disponibilidades no sea hoy, sino el indicado. Por ejemplo se usará si los precios cambian dependiendo de los días que quedan hasta la fecha de la entrada. *Formato ISO 8601 (yyyy-MM-dd)*
- **`LanguageCode`**: `#!csharp string` define el idioma en que se mostrarán los textos del catálogo (nombre/descripción/condiciones de proveedor/producto/). Por defecto se devolverá el idioma configurado para el  colaborador.
- **`ShowProductsOutOfActiveDateRange`**: `#!csharp bool` si su valor es `#!csharp true`, la respuesta devolverá productos en los que el día de hoy (o el día indicado en ReferenceDate) está fuera de su rango de fechas de venta. Por ejemplo, si estamos en diciembre y hay productos que se pueden vender a partir de enero, poniendo este valor a true nos permitirá descubrir que existen esos productos.

### Ejemplos

--8<-- "includes/CatalogQueryExamples.md"
