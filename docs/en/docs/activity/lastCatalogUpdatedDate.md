# Last catalog update date

The product catalog is totally dynamic and can suffer changes. To easily detect changes in the product catalog we have the method **``CatalogLastUpdatedDateTime``**, which will return the date on which the last change was made in the product catalog.

!!! important "Important"
    To know if the catalog has been modified since it was last obtained, we have to compare the date that was obtained from the catalog the last time it was imported and the date obtained in this method.
    !!! success ""
        If the date obtained is less than or equal to the one stored in the catalog that we have processed, we do not have to do anything.
    !!! warning ""
        If the date obtained is greater, that is, more current than the one we have stored, we have to import the catalog again for internal processing.

## Access method

**GET** /activity/cataloglastupdateddatetime

## Response data structure

- **``LastUpdatedDateTime``**: date of the last modification of the catalog. *ISO 8601 format (yyyy-MM-ddThh:mm:ss.fffffff)*.
- **``Success``**: boolean (``#!csharp true/false``) that indicates if the request has been correct or not.
- **``Timestamp``**: time instant of request processing. *ISO 8601 format (yyyy-MM-ddThh:mm:ss.fffffff)*.
- **``ErrorMessage``**: error message explaining why the request was not successful. If it was correct, it will return ``#!csharp null``.

### Ejemplo de respuesta

--8<-- "includes/examples/activity/lastCatalogUpdatedDateResponseExamples.md"
