- **``People``**: (``list``) ``Requerido``. Listado de personas que componen el paquete. El orden en el cual se añaden las personas en este listado repercute, posteriormente, en el índice a usar en la propiedad ``Room``
    - **``Person``**: (``object``) ``Requerido``. Información de la persona.
        - **``Type``**: (``int``) ``Requerido``. Tipo de persona.

            ??? example "Posibles valores"
                --8<-- "includes/enum/personType.md"

        - **``Age``**: (``int``) ``Opcional``. Edad de la persona. Obligatorio, únicamente, si se trata de un niño o bebé (tipo ``1`` y ``2``).