### Sin plugin

_jCrystal_ esta hecho para utilizarse desde *Eclipse*, los pasos para crear un proyecto de _jCrystal_ en Eclipse son:
- Instalar Eclipse
- Instala [el plugin de Cloud Tools para Eclipse](https://cloud.google.com/eclipse/docs/quickstart)
- Crear un proyecto de tipo *XXXXX*
- Añadir en la carpeta  *XXXX* WEB-INF del proyecto los archivos [`jCrystalUtils.jar`](http://jcrystal.crystaltech.co/libs/jCrystalUtils.jar) y `XXXXX`
- Incluir los archivos anteriores en el _build path	_
- Poner en la raíz del proyecto el archivo [`jcrystal.jar`](http://jcrystal.crystaltech.co/libs/jcrystal.jar)
- En la configuración del proyecto en _Eclipse_ en la sección  _Java Compiler_ activar la opción *"Store information about method parameters (usable via reflection)"* (esto permite que los *endpoints* generados tengan nombres de parámetros con significado)
- Crear el archivo de configuración según se describe a continuación.

La configuración de _jCrystal_ debe estar en el paquete por defecto del proyecto, en una clase llamada `JCrystalConfig`, adicionalmente como una salvaguarda para que _jCrystal_ se ejecute debe existir en la carpeta raíz del proyecto un archivo llamado `jcrystal.txt`.

El archivo `JCrystalConfig.java` debe tener un método estático publico sin retorno, donde se define entre otras cosas:
- La IP del servidor de generación de _jCrystal_
- El paquete del proyecto donde se crearan las *clases auxiliares*
- El paquete del proyecto donde se crearan los servlets
- La definición de los clientes para los que se generara una capa de conexión.
    - URL donde se accederá el servicio.
    - Tipo de cliente (según `jcrystal.clients.ClientType`)
    - Carpeta donde se generara el código.
```java
import static jcrystal.JCrystalConfig.*;

import java.io.File;

import jcrystal.clients.Client;
import jcrystal.clients.ClientType;
import jcrystal.clients.JClientMobile;
import jcrystal.json.JsonLevel;

public class JCrystalConfig {
	public static void config(){
		//Estas 4 configuraciones operan sobre los atributos estaticos de jCrystal.JCrystalConfig
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

