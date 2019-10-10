#### El frontend administrador
Existe un tipo de salida que genera un administrador web, que provee funcionalidad CRUD sobre las entidades del backend.  Para implementarlo se debe poner en la clase de configuración `jCrystalConfig`, una salida de tipo ClientType.ADMIN

```java
new Client(ClientType.ADMIN, "admin")
	.setServerUrl(service_url)
	.setOutput("/admin");
```

Para implementarlo se debe crear por cada entidad que se quiera manejar en el administrador una clase Manager con la anotación `@AdminClient`; que debe indicar la clase de la entidad que representa, su nombre para mostrar al usuario, y la ruta que debe tener en el menu (en el siguiente ejemplo: Otros ➡️ Mi Entidad)

`@AdminClient(type=MiEntidad.class, label="Mi Entidad", path="Otros/Mi Entidad")`

##### Metodos del manager de administrador
`list`
`get`
`update`
`delete`
`create`
###### Metodos de lista
Con la anotación `@ListOption`

```java
@ListOption(name="Cambiar flag", icon="lock")
public static String flip(MiEntidad ent) {
	ent.enabled(!ent.enabled()).put();
	return "El 'flag' ha sido " + (ent.enabled()?"encendido":"apagado")+".";
}
```
Este ejemplo cambia el valor de un flag booleano en el objeto `MiEntidad` y lo almacena, ademas retorna un mensaje que se presentara en la interfaz de administración web.

Los iconos posibles son los provistos por [jQuery UI](https://jqueryui.com/themeroller/)(Ver sección Framework Icons)