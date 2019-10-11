## Niveles de acceso
Los campos de una entidad pueden tener niveles de detalle que especifican subconjuntos de campos con los que se puede presentar el objeto.  Un nivel de detalle incluye  todos los niveles inferiores, p.e: si se pide un objeto con nivel de detalle NORMAL, este incluirá también los campos con nivel MIN y BASIC.

Estos son los niveles posibles en **orden**, especificados en el _enum_ `jcrystal.json.JsonLevel`; a saber:
- MIN
- BASIC
- NORMAL: el nivel de acceso por defecto
- DETAIL
- FULL
Además hay tres niveles especiales.
- NONE: Indica que el campo no se debe incluir en ninguna presentación del objeto.
- ID: solo el identificador.
- TOSTRING: el identificador y el resultado del método `toString()` de la entidad.
- DEFAULT: **No debe usarse**, lo usa JCrystal internamente.

En el caso de las propiedades el nombre del parámetro es _json_, en el de las relaciones _keyLevel_.

_Nota:_ estos niveles de acceso se usan de manera paralela en los servicios.