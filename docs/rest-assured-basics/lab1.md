# REST Assured Basics - Lab 1

## 1. Base Test class

The base test class is one test pattern that must be used in any layer.
Let's add the basic RESTAssured configuration:

1. Create a class named `BaseApiConfiguration` in the `se.jfokus.workshop` at `src/test/java/` folder
2. Add the keyword abstract on its declaration
```java
public abstract class BaseApiConfiguration {
}
```
3. Add the configuration necessary to execute any later test:
```java
import io.restassured.RestAssured;
import io.restassured.config.JsonConfig;
import io.restassured.config.RestAssuredConfig;
import io.restassured.path.json.config.JsonPathConfig;
import org.junit.jupiter.api.BeforeAll;

public abstract class BaseApiConfiguration {

    @BeforeAll
    static void mainConfiguration() {
        RestAssured.baseURI = "http://localhost";
        RestAssured.basePath = "/api/v1";
        RestAssured.port= 8088;

        RestAssured.config = RestAssuredConfig.newConfig().
                jsonConfig(JsonConfig.jsonConfig().numberReturnType(JsonPathConfig.NumberReturnType.BIG_DECIMAL));

        RestAssured.enableLoggingOfRequestAndResponseIfValidationFails();;
    }
}
```

## 2. Add the restrictions tests

### 2.1 Create the package to add the restrictions tests

1. Create an additional package called `restriction` in `se.jfokus.workshop` in the `src/test/java` folder

### 2.2 Search for a CPF without restriction

#### :material-play-box-multiple-outline: Steps

1. Create a Java class named `RestrictionsTest` in `se.jfokus.workshop.restriction` in the `src/test/java` folder
2. Make `RestrictionsTest` extends `BaseApiConfiguration`
3. Create a test method named `shouldQueryCpfWithoutRestriction()`
4. Add the following to the test:
  - pre-condition (`given()`) using a path parameter `pathParam` using
    - key: `cpf`
    - value: `1234567890`
  - action (`when()`) to get (`get()`) the `/restrictions/{cpf}` endpoint
  - assert (`then()`) in the status code expecting HTTP 404
    - tip: use `HttpStatus.SC_NOT_FOUND`
5. Run the test

#### :material-checkbox-multiple-outline: Expected results

* Green test execution where the verification of the status code is successfull

#### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    import org.apache.http.HttpStatus;
    import org.junit.jupiter.api.DisplayName;
    import org.junit.jupiter.api.Test;
    import se.jfokus.workshop.BaseApiConfiguration;

    import static io.restassured.RestAssured.given;

    class RestrictionsTest extends BaseApiConfiguration {

        @Test
        @DisplayName("Should query CPF without restriction")
        void shouldQueryCpfWithoutRestriction() {
            given()
                .pathParam("cpf", "1234567890")
            .when()
                .get("/restrictions/{cpf}")
            .then()
                .statusCode(HttpStatus.SC_NOT_FOUND);
        }
    }
    ```
