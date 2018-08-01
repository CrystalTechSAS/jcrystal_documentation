# jcrystal

## Generalidades
_jcrystal_ es un framework de generación de codigo que permite:
- A partir de una definición de entidades, generar metodos de consulta para las mismas
- A partir de una definición de alto nivel de un servicio, generar Servlets que lo atiendad, y conectores para distintos tipos de clientes.
- Validación de usuarios.
## En detalle
### Entidades
Las entidades en _jcrystal_ son clases que se almacenaran en una tabla en la base de datos, para marcarlas se usa la anotación `@Entidad`
#### Campos
`@EntityProperty`
final
##### Relaciones entre entidades

##### Niveles de detalle

#### Indices
Para poder filtrar una _Entidad_ por un campo este debe estar indexado, esto se logra con el parametro indexed colocado en true en la anotación `@EntityProperty` asi:
`@EntityProperty(indexed = true)`


### Pseudoentidades
`@Jsonify`

### Tokens

## Configuración inicial
La configuración de _jcrystal_ debe estar en el paquete por defecto del proyecto, en una clase llamada `JCrystalConfig`, adicionalmente como una salvaguarda para que _jcrystal_ se ejecute debe exister en la carpeta raiz del proyecto un archivo llamado `jcrystal.txt`.

El archivo `JCrystalConfig.java` debe tener un metodo estatico publico sin retorno, donde se define entre otras cosas:
- La IP del servidor de generación de _jcrystal_
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

### Configuración adicional para Angular2
Se debe crear el archivo de configuración en `src/util/app-configuration.ts` con el siguiente contenido
```typescript
export class AppConfiguration{
  static DEBUG = true;
}
```
## Usando jcrystal
### Mecanismo de consulta de la capa de datos
`Famoso.Query.muerto(true)`

### Implementando servicios
Las clases donde se implementan servicios en _jcrystal_  se llaman *managers*, para implementar una de estas clases se deben cumplir dos condiciones:
- El nombre de la clase debe comenzar por `Manager`
- La clase debe estar en un paquete que en algún punto de su ruta contenga una carpeta `controllers` p.e. `app.controllers.auth`

Cada uno de los metodos publicos y estaticos de la clase se convertira en la URL de un servicio respondido por dicho metodo, por este razón no se puede repetir el nombre de un metodo en una clase de servicio.

La URL relativa del servicio resultante se construye a partir de:
- El nombre del subpaquete despues de la carpeta `controllers` p.e. `app.controllers.auth` ➡ `auth`
- El nombre de la clase omitiendo el prefijo `Manager`p.e. `ManagerUser` ➡ `user`
- El nombre del metodo p.e. `public static void create(...) {...}` ➡ `create`
La URL resultante seria entonces `auth/user/create` relativa a la raiz del servicio definida en la configuración.

#### Servicios de validación

#### Recibiendo datos por POST.

## Utilidades
### El metodo asserT
El metodo asserT se encuentra definido en el paquete `jcrystal.utils.ManagerUtils` y permite implementar validaciones en los metodos que retornan un texto, que sera visto por el cliente como un _popup_.

### Fecha y hora
- `CrystalDate`
- `CrystalDateMilis`
- `CrystalDateSeconds`
- `CrystalDateTime`
- `CrystalTime`
- `CrystalTimeMilis`
- `CrystalTimeSeconds`