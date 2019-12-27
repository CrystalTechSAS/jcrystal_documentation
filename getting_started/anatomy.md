# Anatomy of a jCrystal application

The structure of a jCrystal application follows the standardized structure of a Java Web application with some minor changes. After following the [guide to creating a new application](creating_app.md), the project should look like this:

```
pom.xml
src/
└── main/
    ├── java/
    │   └── jCrystalConfig.java
    ├── utils/
    ├── webapp/
    │   ├── META-INF/
    │   ├── WEB-INF/
    │   ├── index.html
    │   └── favicon.ico
    └── test/java/ 
```


### The **`pom.xml`** file
This file contains configuration details and dependencies used by Maven to build the project. Any external dependency should be added here.

For more information on this file check this [link](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html).

### The **`src/main/java/`** directory

This folder contains all your folder source code. Here you will write your entities, managers and everything you need for your app. 


### The **`src/main/java/jCrystalConfig.java`** file

This file contains the main configuration of a jCrystal project. It must **always** be present on your project at the root of this folder: `src/main/java`.
 
In this file, you configure:

- The clients that this project will use.
- The service URL that will hold your server and that will be used to generate the integration code for your clients.
- More.

### The **`src/main/utils/`** directory
This folder is used to store almost all the generated classes from jCrystal. Feel free to checkout what jCrystal generates, however you **mustn't change or alter these files**; if you do, the next time you run jCrystal those changes will be lost. 

### The **`src/main/webapp/`** directory

This folder contains web pages, CSS or images of your web application. If you want to use the same domain for your backend and your frontend application, you will have to update the static files found in here:
- index.html
- favicon.ico

If your backend and frontend can have different domains, you don't need to change these files.

For more information on this directory check this [link](https://docs.oracle.com/javaee/7/index.html).

### The **`src/main/webapp/WEB-INF`** folder

This folder contains configuration files of your application. Usually, you don't need to add or change any file here.

### The **`src/main/webapp/META-INF`** folder
This folder contains internal project files. You don't need to add or change any file here.

### The **`src/test/java`** folder
This is a default folder that contains the tests of the project. It is not used by jCrystal. 
