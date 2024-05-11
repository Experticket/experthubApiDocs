- **``Filter``**: (``list``) ``Opcional``. Filtros para acotar el resultado. Los distintos filtros se añaden como si de un operador ``AND`` se tratase.
    - **``AccommodationBoards``**: (``list``) ``Opcional``. Listado con los regímenes del alojamiento deseados.
        - **``(int)``**: ``Opcional``. Tipo de régimen alimenticio.

          ??? example "Posibles valores"
          --8<-- "includes/enum/accommodationBoard.md"

    - **``AccommodationCategories``**: (``list``) ``Opcional``. Listado con las categorías del alojamiento deseadas.
        - **``(int)``**: ``Opcional``. Tipo de categoría del alojamiento.

          ??? example "Posibles valores"
          --8<-- "includes/enum/accommodationCategory.md"

    - **``AccommodationRateClasses``**: (``list``) ``Opcional``. Listado de alojamientos con o sin reembolso.
        - **``(int)``**: ``Opcional``. Indica si se quiere o no con reembolso.

          ??? example "Posibles valores"
          --8<-- "includes/enum/accommodationRateClass.md"

    - **``AccommodationTypes``**: (``list``) ``Opcional``. Listado de tipos de alojamiento.
        - **``(int)``**: ``Opcional``. Indica el tipo de alojamiento.

          ??? example "Posibles valores"
          --8<-- "includes/enum/accommodationType.md"

    - **``Cities``**: (``list``) ``Opcional``. Listado de ciudades.
        - **``(string)``**: ``Opcional``. Nombre de la ciudad.

    - **``PriceRange``**: ``Opcional``. Rango de precios del paquete. En caso de más de un elemento, actuarán como un operador de unión ``OR``.
       - **``Min``**: (``int``) ``Opcional``. Precio mínimo.
       - **``Max``**: (``int``) ``Opcional``. Precio máximo.