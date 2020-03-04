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
DONE

### Roles
Solo puede haber uno en toda la aplicación.
`@RolEnum`

ids potencias de 2, mascaras