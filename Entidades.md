# Entidades
## Introducción
Una entidad en JCrystal comienza como una clase con la definición de un objeto con ciertas propiedades, relaciones y comportamientos; las instancias de esta entidad se almacenaran en un tabla en un Datastore de GAE.

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
Cuando se usa un `enum` como atributo de una entidad, este debe tener un método estático que devuelve un elemento a partir de un identificador entero con el nombre `fromId`.  El identificador se utiliza para transmitir la información y almacenarla en la base de datos.

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

#### Índices
Para poder filtrar una _Entidad_ por un campo este debe estar indexado, esto se logra con el parámetro indexed colocado en true en la anotación `@EntityProperty` así:
`@EntityProperty(indexed = true)`

##### Índices complejos
`@Index`

### Pseudoentidades
`@Jsonify`

### Tokens

## Especificación
Para indicar que una clase es una entidad de JCrystal, se debe anotar con `@jcrystal.reflection.annotations.Entidad`
-TODO- Parámetros.

### Campos de la entidad
Los campos de la entidad se especifican con atributos estáticos; para evitar confusiones, se recomienda que se declaren como `private`.

Entre los métodos que genera JCrystal para los campos están los _getters_ y los _setters_ de cada uno de los campos.

Para que un campo sea __requerido en el constructor__, su especificación debe especificar con la palabra clave _final_.

#### Propiedades
Las propiedades de la entidad son aquellos campos que no expresan una relación con otra entidad, sus tipos pueden ser:
- Tipos primitivos de Java
- Arreglos de tipos primitivos
- Clases Wrapper de tipos primitivos.
- Arreglos de wrappers de tipos primitivos
- String
- Email -TODO- Clase exacta
- GeoPt De Google
- los _wrapper_ de JCrystal para las fechas (CrystalDate).

Se denotan con la anotación `@jcrystal.reflection.annotations.EntityProperty`

-TODO- Preguntar GA tipos soportados

##### Parámetros
La anotación `@jcrystal.reflection.annotations.EntityProperty` tiene los siguientes parámetros.
- _name_ (String): nombre interno que se usara para el campo el la tabla del Datastore.
- _unique_ (booleano): indica si se espera que solo haya un resultado por cada valor de la propiedad, los métodos de consulta usando esta propiedad retornaran un solo resultado en vez de una lista de ellos.
- _indexed_ (booleano): Indica si la variable esta indexada, lo cual es requisito para que se puedan buscar en la base de datos registros con un valor especifico de la misma.
- _editable_
- _json_
- _autoNow_ (booleano): aplicable solo a los parámetros de tipos CrystalDate*, indica si estos se inicializan automáticamente con el tiempo actual.

#### Relaciones
Las relaciones son campos de una entidad que la asocian con otra, pueden ser '1 a 1', 'muchos a muchos' o 'muchos a 1', estos campos se denotan con las siguientes anotaciones [todas del paquete `jcrystal.reflection.annotations.entities`]:
- `@Rel1to1`
- `@RelMto1`
- `@RelMtoM`

Todas comparten los mismos parámetros:
- _name_(String): equivalente al parámetro del mismo nombre en las propiedades
- _target_(String): nombre del pseudo-campo que se creara en la entidad referida con la relación inversa.
- _keyLevel_: equivalente al parámetro _json_ en las propiedades
- _editable_(boolean): equivalente al parámetro del mismo nombre en las propiedades

Los campos de relación, son indexados automáticamente y por tanto no tienen la opción _indexed_.

### Índices
Como se indico previamente, las propiedades de una entidad pueden estar indexadas, en la caso de las propiedades de manera optativa y en el de las relaciones de manera automática.

Sin embargo, en algunos casos se necesita buscar registros no por el valor de un campo sino por la combinación de valores de varios campos, en estos casos la clase de la entidad se anota con `@EntityIndex` con los siguientes parámetros:
- _name_: nombre cual el cual se referirá
- _value_: Un arreglo de String con los nombres internos de los campos incluidos en el índice.

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

## Métodos
Tras la primera ejecución de JCrystal se pueden implementar métodos auxiliares que no serán modificados por JCrystal.

### Métodos de inicialización @jcrystal.reflection.annotations.entities.OnConstruct
Los métodos anotados con `@OnConstruct` son llamados desde el constructor del objeto y se usan comúnmente para inicializar el valor de las propiedades.

### Representación como cadena de texto toString
Cuando se usa el nivel de acceso JsonLevel.TOSTRING, el objeto resultante solo contiene el resultado de su método toString y su identificador.

### Métodos generados

#### Constructor
El constructor incluye los parámetros que hayan sido marcados como obligatorios (con _final_) en la declaración de la entidad.  Y cambien a los métodos con la anotación @OnConstruct

Un ejemplo:

#### Setters y getters

## Funciones de consulta
Subclase Query
### Subclase query

## Objetos DAO, según niveles de acceso.



### Nota sobre la generación del código
Una parte del código que genera JCrystal para la entidad se crea dentro del mismo archivo de clase que contiene la definición.

Este código generado se coloca dentro de unos comentarios que delimitan la sección generada, para que en ejecuciones posteriores del generador de código se sobrescriba solo la región generada.

Un ejemplo:
```java
@Entidad
public class Room {
  //Aqui se encuentra la especificación.
/* GEN */
 //Aqui se encuentra el codigó generado.
/* END */
}
```
