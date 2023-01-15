# Setup - Project

In this lab, we will create the BaseTest class and the basic tests related to Restrictions API.

## 1. Create a new project

1. Open your preferred IDE
2. Create a new Java project:
  - based on Maven
  - named `credit-api-tests`
  - you can name any group, but I recommend you using `se.jfokus.workshop` 

## 2. Adding the libraries

We need to add the base dependencies to start creating the tests.

1. Open the `pom.xml` file and add the following dependencies
```xml
<project>
    <!-- code ignored-->

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.target>18</maven.compiler.target>
        <maven.compiler.source>18</maven.compiler.source>
        <junit.version></junit.version>
    </properties>

    <dependencies>

        <!-- JUnit 5 -->
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>5.9.2</version>
        </dependency>

        <!-- RestAssured library -->
        <dependency>
            <groupId>io.rest-assured</groupId>
            <artifactId>rest-assured</artifactId>
            <version>5.3.0</version>
        </dependency>

        <!-- Assertion library -->
        <dependency>
            <groupId>org.assertj</groupId>
            <artifactId>assertj-core</artifactId>
            <version>3.24.1</version>
            <scope>test</scope>
        </dependency>

        <!-- Data generation library -->
        <dependency>
            <groupId>net.datafaker</groupId>
            <artifactId>datafaker</artifactId>
            <version>1.7.0</version>
            <scope>test</scope>
        </dependency>

    </dependencies>
</project>    
```

### 2.1 Libraries latest versions

| Library      | Version |
|--------------|---------|
| Rest-Assured | [![JUnit](https://maven-badges.herokuapp.com/maven-central/org.junit.jupiter/junit-jupiter/badge.svg?style=flat)](http://mvnrepository.com/artifact/org.junit.jupiter/junit-jupiter) |
| Rest-Assured | [![Rest-Assured](https://maven-badges.herokuapp.com/maven-central/io.rest-assured/rest-assured/badge.svg?style=flat)](http://mvnrepository.com/artifact/io.rest-assured/rest-assured) |
| AssertJ | [![AssertJ](https://maven-badges.herokuapp.com/maven-central/org.assertj/assertj-core/badge.svg?style=flat)](http://mvnrepository.com/artifact/org.assertj/assertj-core) |
| DataFaker | [![DataFaker](https://maven-badges.herokuapp.com/maven-central/net.datafaker/datafaker/badge.svg?style=flat)](http://mvnrepository.com/artifact/net.datafaker/datafaker) | 

## 3. Make sure you have the following project structure

You must have the following structure in your project:
```
─── src
    ├── main
    │   └── java
    │       └── se.jfokus.workshop
    └── test
        ├── java
        │   └── se.jfokus.workshop
        └── resources
```
