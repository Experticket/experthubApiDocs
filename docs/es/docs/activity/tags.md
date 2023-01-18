# Etiquetas

Las etiquetas sirven para categorizar proveedores según el tipo de ocio que ofrecen, por ejemplo: *Parques temáticos*, *Espectáculos*, *Museos*, *Conciertos*, etc.

Los identificadores de las etiquetas asignadas se pueden ver en el [catálogo](catalog.md) a nivel de proveedor.

## Método de acceso

**GET** /activity/tags

## Estructura de la petición

- **``LanguageCode``** (`string`): identificador del idioma con el que queremos obtener las etiquetas. *Formato ISO 639-1*.

### Ejemplos de petición

--8<-- "includes/examples/activity/tagsQueryExamples.md"

## Estructura de la respuesta

- **``Tags``** (`list`): array de etiquetas.
    - **`Tag`** (`object`): etiqueta.
        - **``Id``** (``string``): identificador de la etiqueta. Alfanumérico de 13 caracteres.
        - **``Key``** (``int``): clave de la etiqueta. Valor entero único entre todas las etiquetas.
        - **``Name``** (``string``): nombre de la etiqueta (por ejemplo "*Teatros y espectáculos*").
        - **``PathName``** (``string``): ruta de la etiqueta separada por "/" en el caso de que tenga etiquetas hijas (por ejemplo "Teatros y espectáculos / Conciertos").
        - **``Children``** (``list``): etiquetas hijas de la etiqueta actual. El nivel de anidamiento es infinito, puede haber etiquetas con profundidad de N hijas. La estructura de las etiquetas hijas es la misma que las etiquetas padre.

--8<-- "includes/responseBaseDocumentation.es.md"

### Ejemplo de respuesta

--8<-- "includes/examples/activity/tagsResponseExamples.md"
