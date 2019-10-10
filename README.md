# jCrystal Framework
_jCrystal_ is a fullstack framework based on code generators. It aims to reduce code re-write on web applications by reuseing backend side data structures, business logic and web services to generate frontend equivalents.

## What can you achieve with jCrystal?
On the Server Side:
- Build a Object-Relactionship Model for yours clases and deploy it on a Non-SQL Database.
- Bulld Restful Web Services endpoints and deploy them on a HA infrasestructure.
- Process async job loads in a simple way.
- Validación de usuarios.

* Our MVP allows you to write your backend in Java and deploy it over Google App Engine using Google Datastore database (legacy).

On the Client Side:
Los *endpoints* se pueden generar como:
- Swift para iOs
- Java para Android
- Typescript para plataformas web (especialmente Angular2)

jCrystal have support for the following platforms:
- iOS 12^ (Using Swift 5)
- Android 6^ (Using Java 8^)
- Flutter (Using Dart)
- Angular 7^(Usign Typescript)
- jQuery (using JS)

## jCrystal layers:
We propose (an generate?) 3 simple layers:

- A data access layer: it allows access to stored data in all platforms.
- A connection layer: composed by RestfulWS, it allows communication between platforms
- Buisiness layer?

- [Entidades](Entidades.md)
- [Servicios](Servicios.md)

## Installation

- [Using Eclipse](Installation.md)

### Configuración adicional para Angular2
Se debe crear el archivo de configuración en `src/util/app-configuration.ts` con el siguiente contenido
```typescript
export class AppConfiguration{
  static DEBUG = true;
}
```
#### Dependencias
El código generado para Typescript depende de estas librerías:
- [moment](https://www.npmjs.com/package/moment)
- [sweetalert](https://www.npmjs.com/package/sweetalert)
Adicionalmente se debe incluir la librería XXXXX en el modulo principal.

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
Cada uno de los métodos públicos y estáticos de la clase se convertirá en la URL de un servicio respondido por dicho método, por este razón no se puede repetir el nombre de un método en una clase de servicio.

La URL relativa del servicio resultante se construye a partir de:
- El nombre del subpaquete después de la carpeta `controllers` p.e. `app.controllers.auth` ➡ `auth`
- El nombre de la clase omitiendo el prefijo `Manager`p.e. `ManagerUser` ➡ `user`
- El nombre del método (palabras separadas por _underscore_ se convierten en otra parte de la ruta) p.e. `public static void admin_create(...) {...}` ➡ `admin/create`
La URL resultante seria entonces `auth/user/admin/create` relativa a la raíz del servicio definida en la configuración.

#### Generando *endpoints* para los clientes
Para que se generen los *endpoints* de los servicios para un determinado cliente, se debe agregar una anotación de la forma `@<nombre_cliente>Client` donde nombre_cliente es uno de los definidos en el archivo de configuración de jCrystal.  Esta anotación puede colocarse:
- En el [paquete](https://docs.oracle.com/javase/specs/jls/se8/html/jls-7.html) para abarcar todos los métodos de los Managers en el.
- En la clase para abarcar todos los métodos del Manager.
- En un método para abarcar solo ese método.

#### Servicios de autenticación

#### Recibiendo datos por POST.

#### Campos obligatorios.
Los campos obligatorios se indican con un underscore(_) al final del nombre del parámetro, por ejemplo, el siguiente método:
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
El método asserT se encuentra definido en el paquete `jcrystal.utils.ManagerUtils` y permite implementar validaciones en los metodos que retornan un texto, que será visto por el cliente como un _popup_.  El metodo recibe una condición y un mensaje, cuando la condicióm es falsa se arroja una excepción y se interrumpe la ejecución del metodo.

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

Los iconos posibles son los provistos por [jQuery UI](https://jqueryui.com/themeroller/)(Ver sección Framework Icons)

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
