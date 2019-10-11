###### Ejemplo completo

#### Temas pendientes
- @CarbonCopy
- @ListOption en los métodos de los manager `@ListOption(name="nueva membresía", icon="dollar-sign")`
- @JsonString en los métodos de los manager
- @RelMTo1 implica que el campo se puede filtrar
- En el metodo generado `Entidad.PostNormal.validate` el método validate debería aplicar las validaciones que se implementan en la entidad
- Las tildes y las ñ no son toleradas
- `LongText` ~~es~~ era un tipo que remplaza String para textos largos
- En Android se requiere que exista la clase aplication de la Aplicación.

[App Engine Client For Google Cloud Storage](https://mvnrepository.com/artifact/com.google.appengine.tools/appengine-gcs-client)
- Que a su vez requiere [Guava](https://mvnrepository.com/artifact/com.google.guava/guava)


###### Cambios primero de septiembre
- Ahora en la configuración (JCrystalConfig) se puede activar el modo debug del servidor con `SERVER.DEBUG = true;`, por defecto dicho modo esta desactivado.
- SERVER.servlet_root_path = "";
- @NombreDeLaEntidad.Meta.Order({NombreDeLaEntidad.Meta.M.campo1,NombreDeLaEntidad.Meta.M.campo2})