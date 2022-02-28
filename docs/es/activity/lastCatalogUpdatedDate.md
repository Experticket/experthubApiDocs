# Última fecha de actualización de catálogo

El catálogo de productos es totalmente dinámico y puede sufrir cambios. Para detectar fácilmente cambios en el catálogo de productos tenemos el método **``CatalogLastUpdatedDateTime``**, que nos devolverá la fecha en la que se ha realizado el último cambio en el catálogo de productos.

!!! important "Importante"
    Para conocer si se ha modificado el catálogo desde su última obtención tenemos que comparar la fecha que se obtuvo del catálogo la última vez que se importó y la fecha obtenida en este método.
    !!! success ""
        Si la fecha obtenida es menor o igual a la almacenada en el catálogo que hayamos procesado no tenemos que hacer nada.
    !!! warning ""
        Si la fecha obtenida es mayor, es decir, más actual que la que tenemos almacenada debemos importar de nuevo el catálogo para su procesamiento interno.

## Método de acceso

**POST** /activity/cataloglastupdateddatetime

## Estructura de datos de respuesta

- **``LastUpdatedDateTime``**: fecha de la última modificación del catálogo. *Formato ISO 8601 (yyyy-MM-ddThh:mm:ss.fffffff)*.
- **``Success``**: booleano (``#!csharp true/false``) que indica si la petición ha sido o no correcta.
- **``Timestamp``**: instante de tiempo del procesamiento de la solicitud. *Formato ISO 8601 (yyyy-MM-ddThh:mm:ss.fffffff)*.
- **``ErrorMessage``**: mensaje de error explicando por qué la petición no ha sido correcta. En caso que haya sido correcta, devolverá ``#!csharp null``.

### Ejemplo de respuesta

--8<-- "includes/examples/activity/lastCatalogUpdatedDateResponseExamples.md"
