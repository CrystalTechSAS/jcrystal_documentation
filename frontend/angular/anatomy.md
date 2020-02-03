# Anatomy of the jCrystal generated folder
The generated folder of jCrystal in Angular looks like this:

```
jcrystal/
├── entities/
│   ├── enums/
│   └── jCrystalConfig.java
├── services/
└── JSONUtils.ts
```

Feel free to look at each of the files and folders, but remember that since this is a generated folder, any change on these files will be removed the next time the code is generated.

### The **`jcrystal/entities`** folder

The entities folder contains all the .ts files of the data models that are used by the web services of your client. 

Please take into account that this means that not all the jEntities on the backend are generated on typescript, jCrystal only creates the data models that are needed because they are used on some web service.

### The **`jcrystal/entities/enums`** folder
This folder contains the .ts files of the enumerations that are used by the web services of your client. This folder might not be generated if the backend doesn't use any enumeration.

### The **`jcrystal/services`** folder
This folder contains the .ts files of the web services used by your client and some helper classes to consume those web services.
The classes that you need to use to consume the web services start with "Manager"; inside of them, you will find static methods, each of them calls a web service.

### The **`JSONUtils.ts`** file
This file contains utilities to transform objects into JSON. You don't need to use this class.