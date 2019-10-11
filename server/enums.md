# Enums como atributos de una entidad
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