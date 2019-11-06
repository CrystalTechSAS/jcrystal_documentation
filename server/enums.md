# Enums for entity fields

You can use enums as field types for your entities. For now, every enum should have a _public long id_ to unique identify each object and a method to retrieve the object given the id.

This is a example of a valid enum for jCrystal:
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