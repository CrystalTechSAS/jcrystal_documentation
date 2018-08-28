# jCrystal
_jCrystal_ es un framework de generación de codigo, para aplicaciones web cuyo principal objetivo es minimizar la rescritura de estructuras de datos, logica de negocio y sintaxis de los servicios entre el backend y los distintos frontend que puede tener la aplicación.

## Generalidades
_jCrystal_ que permite:
- A partir de una definición de entidades, generar metodos de consulta para las mismas
- A partir de una definición de alto nivel de un servicio, generar Servlets que lo atiendad, y conectores para distintos tipos de clientes.
- Validación de usuarios.

_jCrystal_ esta escrito en Java, y esta hecho para funcionar sobre Google App Engine con *XXXXX* como base de datos.

El backend generado funciona con Servlets de Java EE.

Los *endpoints* se pueden generar como:
- Swift para iOs
- Java para Android
- Typescript para plataformas web (especialmente Angular2)

Las capas presentes en la arquitectura de jCrystal son:
- Datos, mediante la definición de _Entidades_
- Logica, mediante la definición de _Crystals_
- Web Services, mediante la definición de _Managers_
- *Resources*
Sin embargo en la mayoria de casos la capa de logica es prescindible, y la capa de los Web Services utiliza directamente la capa de datos.

## En detalle
### Entidades
Las entidades en _jCrystal_ son clases que se almacenaran en una tabla en la base de datos, para marcarlas se usa la anotación `@Entidad`

Otras anotaciones que puede tener una entidad `@Entidad` son `@CarbonCopy`

#### Campos
`@EntityProperty`

| Parametro     | Tipo          | Descripción  |
| ------------- |-------------| -----|
| indexed     | boolean | Indica si este campo esta indexado en la BD |
| unique     | boolean | Indica si el valor de esta campo no puede repetirse entre objetos de la entidad *OJO: la capa de datos no hace respetar esto*|
| editable     | boolean | ????? |

final
##### Relaciones entre entidades
`@Rel1to1`
`@RelMto1`
`target="x"`
`@RelMtoM`
`small=true` menos de 4000

Los campos de relación no tienen nivel por defecto.

##### Niveles de detalle

##### Enums como atributos de una entidad
Cuando se usa un `enum` como atributo de una entidad, este debe tener un metodo estatico que devuelve un elemento a partir de un identificador entero con el nombre `fromId`.  El identificador se utiliza para transmitir la información y almacenarla en la base de datos.

Un ejemplo de un `enum` que puede ser usado como atributo en una entidad:
```java
public enum StatusType {
	PENDING(1),CONNECTING(2),COMPLETED(3);
	public final int id;
	private StatusType(int id) {
		this.id = id;
	}
	public static StatusType fromId(int id) {
		for (StatusType val: StatusType.values()) {
			if (val.id==id) {
				return val;
			}
		}
		return null;
	}
}
```

#### Indices
Para poder filtrar una _Entidad_ por un campo este debe estar indexado, esto se logra con el parametro indexed colocado en true en la anotación `@EntityProperty` asi:
`@EntityProperty(indexed = true)`

##### Indices complejos
`@Index`

### Pseudoentidades
`@Jsonify`

### Tokens

## Configuración inicial
_jCrystal_ esta hecho para utilizarse desde *Eclipse*, los pasos para crear un proyecto de _jCrystal_ en Eclipse son:
- Instalar Eclipse
- Instala [el plugin de Cloud Tools para Eclipse](https://cloud.google.com/eclipse/docs/quickstart)
- Crear un proyecto de tipo *XXXXX*
- Añadir en la carpeta  *XXXX* WEB-INF del proyecto los archivos `jCrystalUtils.jar` y `XXXXX`
- Incluir los archivos anteriores en el _build path_
- Poner en la raiz del proyecto el archivo `jcrystal.jar`
- En la configuración del proyecto en _Eclipse_ en la sección  _Java Compiler_ activar la opción *"Store information about method parameters (usable via reflection)"* (esto permite que los *endpoints* generados tengan nombres de parametros con significado)
- Crear el archivo de configuración según se describe a continuación.

La configuración de _jCrystal_ debe estar en el paquete por defecto del proyecto, en una clase llamada `JCrystalConfig`, adicionalmente como una salvaguarda para que _jCrystal_ se ejecute debe exister en la carpeta raiz del proyecto un archivo llamado `jcrystal.txt`.

El archivo `JCrystalConfig.java` debe tener un metodo estatico publico sin retorno, donde se define entre otras cosas:
- La IP del servidor de generación de _jCrystal_
- El paquete del proyecto donde se crearan las *clases auxiliares*
- El paquete del proyecto donde se crearan los servlets
- La definición de los clientes para los que se generara una capa de conexión.
    - URL donde se accedera el servicio.
    - Tipo de cliente (según `jcrystal.clients.ClientType`)
    - Carpeta donde se generara el codigo.
```java
import static jcrystal.JCrystalConfig.*;

import java.io.File;

import jcrystal.clients.Client;
import jcrystal.clients.ClientType;
import jcrystal.clients.JClientMobile;
import jcrystal.json.JsonLevel;

public class JCrystalConfig {
	public static void config(){
		//Estas 4 configuraciones operan sobre los atributos estaticos de jcrystal.JCrystalConfig
		JCRYSTAL_SERVER_IP =  "35.229.125.17";
		SERVER_PORT = 80;
		SERVER.setPackageInterfaces("myproject.servlets");
		SERVER.setServletPackage("myproject.servlets");
		
		new Client(ClientType.ADMIN, "admin")
			.setServerUrl("/api/");
		
		new Client(ClientType.TYPESCRIPT, "web")
			.setOutput("/Users/gasotelo/myproject/web/src/app")
			.setServerUrl("https://localhost/api/");
		
		new JClientMobile("mobile")
			.setOutputAndroid("/Users/user/myproject/android/app/src/main/java")
			.setOutputiOS("/Users/user/myproject/ios/jcrystal")
			.setServerUrl("https://localhost/api/");
	}
}
```

El puerto por defecto de jCrystal es el 80.

### Configuración adicional para Angular2
Se debe crear el archivo de configuración en `src/util/app-configuration.ts` con el siguiente contenido
```typescript
export class AppConfiguration{
  static DEBUG = true;
}
```
#### Dependencias
El codigo generado para typescript depende de estas librerias:
- [moment](https://www.npmjs.com/package/moment)
- [sweetalert](https://www.npmjs.com/package/sweetalert)
Adicionalmente se debe incluir la libreria XXXXX en el modulo principal.

## Usando jcrystal
### Mecanismo de consulta de la capa de datos
`Famoso.Query.muerto(true)`
*RANGOS*
*GUARDAR*

### Implementando servicios
Las clases donde se implementan servicios en _jCrystal_  se llaman *managers*, para implementar una de estas clases se deben cumplir dos condiciones:
- El nombre de la clase debe comenzar por `Manager`
- La clase debe estar en un paquete que en algún punto de su ruta contenga una carpeta `controllers` p.e. `app.controllers.auth`

#### La URL del servicio
Cada uno de los metodos publicos y estaticos de la clase se convertira en la URL de un servicio respondido por dicho metodo, por este razón no se puede repetir el nombre de un metodo en una clase de servicio.

La URL relativa del servicio resultante se construye a partir de:
- El nombre del subpaquete despues de la carpeta `controllers` p.e. `app.controllers.auth` ➡ `auth`
- El nombre de la clase omitiendo el prefijo `Manager`p.e. `ManagerUser` ➡ `user`
- El nombre del metodo (palabras separadas por _underscore_ se convierten en otra parte de la ruta) p.e. `public static void admin_create(...) {...}` ➡ `admin/create`
La URL resultante seria entonces `auth/user/admin/create` relativa a la raiz del servicio definida en la configuración.

#### Generando *endpoints* para los clientes
Para que se generen los *endpoints* de los servicios para un determinado cliente, se debe agregar una anotación de la forma `@<nombre_cliente>Client` donde nombre_cliente es uno de los definidos en el archivo de configuración de jCrystal.  Esta anotación puede colocarse:
- En el [paquete](https://docs.oracle.com/javase/specs/jls/se8/html/jls-7.html) para abarcar todos los metodos de los Managers en el.
- En la clase para abarcar todos los metodos del Manager.
- En un metodo para abarcar solo ese metodo.

#### Servicios de autenticación

#### Recibiendo datos por POST.

#### Campos obligatorios.
Los campos obligatorios se indican con un underscore(_) al final del nombre del parametro, por ejemplo, el siguiente metodo:
```java
public static Token login(String email_, String password_) {
	//...
}
```

## Utilidades
### Niveles de detalle
`ClientLevel`

### Niveles de error

MIN BASIC DETAIL NONE
### El metodo asserT
El metodo asserT se encuentra definido en el paquete `jcrystal.utils.ManagerUtils` y permite implementar validaciones en los metodos que retornan un texto, que sera visto por el cliente como un _popup_.  El metodo recibe una condición y un mensaje, cuando la condicióm es falsa se arroja una excepción y se interrumpe la ejecución del metodo.

| Parametro     | Tipo          | Descripción  |
| ------------- |-------------| -----|
| condicion     | boolean | Condición que se valida |
| mensaje      | String      |   Mensaje que se envia si la condición es falsa |


### Fecha y hora
Para el manejo de eventos temporales _jCrystal_ no usa los objetos nativos de cada plataforma sino que implementa en cada una las siguientes clases de utilidad:
- `CrystalDate`
- `CrystalDateMilis`
- `CrystalDateSeconds`
- `CrystalDateTime`
- `CrystalTime`
- `CrystalTimeMilis`
- `CrystalTimeSeconds`

### Roles
Solo puede haber uno en toda la aplicación.
`@RolEnum`

ids potencias de 2, mascaras


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

Los iconos posibles son los proveidos por [jQuery Mobile](https://api.jquerymobile.com/icons/)

###### Ejemplo completo

#### Temas pendientes
- @CarbonCopy
- @ListOption en los metodos de los managager `@ListOption(name="nueva membresía", icon="dollar-sign")`
- @JsonString en los metodos de los managager
- @RelMTo1 implica que el campo se puede filtrar
- En el metodo generado `Entidad.PostNormal.validate` el metodo validate deberia aplicar las validaciones que se implementan en la entidad
- Las tildes y las ñ no son toleradas
- `LongText` ~~es~~ era un tipo que remplaza String para textos largos
- En Android se requiere que exista la clase aplication de la Aplicación.

[App Engine Client For Google Cloud Storage](https://mvnrepository.com/artifact/com.google.appengine.tools/appengine-gcs-client)
- Que a su vez requiere [Guava](https://mvnrepository.com/artifact/com.google.guava/guava)