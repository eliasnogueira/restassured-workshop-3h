# RestAssured Basics Lab

## Libraries

1. Open the `pom.xml` file and add the following dependencies
```xml
<!-- main RestAssured library -->
<dependency>
    <groupId>io.rest-assured</groupId>
    <artifactId>rest-assured</artifactId>
    <version>${restassured.version}</version>
</dependency>

<!-- Assertion library -->
<dependency>
    <groupId>org.assertj</groupId>
    <artifactId>assertj-core</artifactId>
    <version>${assertj.version}</version>
    <scope>test</scope>
</dependency>

<!-- Data generation library -->
<dependency>
    <groupId>net.datafaker</groupId>
    <artifactId>datafaker</artifactId>
    <version>${datafaker.version}</version>
    <scope>test</scope>
</dependency>
```

## Structure
We will create different packages at `src/test/java` folder in the `com.eliasnogueira.credit` package.


