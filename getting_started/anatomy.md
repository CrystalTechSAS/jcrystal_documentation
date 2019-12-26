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

The function of each files and folders of this project is explained here:

| File/Folder                       | Purpose |
|-----------------------------------|---------|
| pom.xml                           | This file contains information about the project, depedencies and other details used by Maven to build the project. Any external depedency should be added here. <br> For more information check this [link](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html)     |
| src/main/java                     |         |
| src/main/java/jCrystalConfig.java |         |
| src/main/utils/                   |         |
| src/main/webapp/                  |         |
| src/main/webapp/META-INF/         |         |
| src/main/webapp/WEB-INF/          |         |
| src/main/webapp/index.html        |         |
| src/main/webapp/favicon.ico       |         |
| src/test/java/                    |         |