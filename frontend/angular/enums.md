# Enumerations

jCrystal generates the .ts files of the enumerations required to communicate with the backend, you can find them in the jCrystal generated folder: `jcrystal/enums`. Each enumeration used by the web services generates one class in typescript with the same attributes that the enumeration has on the backend. 

All the values of an enumeration have at least two attributes by default: `id` and `rawName`; those attributes help you identify each value of the enumeration. Also, by default jCrystal generates the static method `getFromId` to help you get an enumeration value from an id (this could be a number or a string). 

This is an example of a generated enumeration:
```typescript
export class Rol{
	public static OWNER = new Rol('OWNER', 'OWNER');
	public static BACKEND = new Rol('BACKEND', 'BACKEND');
	public static CLIENT = new Rol('CLIENT', 'CLIENT');
	public constructor(public id : string, public rawName : string){}
	static getFromId(id : string) : Rol{
		if ('OWNER' == id) {return Rol.OWNER}
		if ('BACKEND' == id) {return Rol.BACKEND}
		if ('CLIENT' == id) {return Rol.CLIENT}
	}
	static values = [Rol.OWNER, Rol.BACKEND, Rol.CLIENT];
}
```

As you can see, given an instance of this class, you can access its attributes directly like this:
```typescript
import { Rol } from 'src/app/jcrystal/entities/enums/Rol';
...
const rol = Rol.CLIENT;
const idRol:string = rol.id;
const rawNameRol:string = rol.rawName;
```
Whenever you use an enum, don't forget to import the class.

Additionally, you can look up a value of the enumeration given an id:
```typescript
import { Rol } from 'src/app/jcrystal/entities/enums/Rol';
...
const rol = Rol.getFromId('CLIENT');
```
Please take into account that type of the parameter `id` may change (can be number or string) and depends on how the enumeration is defined on the backend. The best way to know what kind of type this method requires is to check the signature of the method on the generated enumeration class.

You can get all the values of the enumeration like this:
```typescript
import { Rol } from 'src/app/jcrystal/entities/enums/Rol';
...
const roles:Rol[] = Rol.values;
```

Please take into account that not all the enumerations created on the backend are generated on your frontend, just the ones that are required to communicate with your backend in any web service.