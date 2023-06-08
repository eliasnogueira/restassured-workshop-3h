# Request and Response Specification - Lab 1

## 1. Creating a generic request specification

### :material-play-box-multiple-outline: Steps

1. Create a package `specs` inside the `com.workshop` at `src/main/java`
2. Create a class called `SharedRequestSpecs` in the `com.workshop.specs` package
3. Create a `public static` method called `cpfPathParameter` adding the parameter `String cpf` to it
4. Inside the method build a request specification add the path parameter to it, fix the `cpf` parameter name, and add the method parameter as its value

!!! tip "Tips"
    The method in step 3 will look like this:
    ```java
    public static RequestSpecification cpfPathParameter(String cpf) {
    }
    ```


    The content of the method in step 4 will look like this:
    ```java
    return new RequestSpecBuilder().addPathParams("cpf",cpf).build();
    ```

### :material-checkbox-multiple-outline: Expected results

- Just the class creation 😊

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    public class SharedRequestSpecs {

        public static RequestSpecification cpfPathParameter(String cpf) {
            return new RequestSpecBuilder().addPathParams("cpf",cpf).build();
        }
    }
    ```

## 2. Modify the tests in the `RestrictionsTest` class

### :material-play-box-multiple-outline: Steps

1. Open the `RestrictionsTest` class located at `src/test/java` in the `com.workshop.restriction` package
2. In both tests: 
     - replace the `pathParam()` method by the `spec()` method
     - use the `cpfPathParameter()` from the `SharedRequestSpecs` class
     - don't forget to keep the same data (`cpf`) in both tests
3. Run the tests

### :material-checkbox-multiple-outline: Expected results

- Green test execution where the following verifications will be performed successfully
    - status code
    - response body

### :material-check-outline: Solution

??? example "Click to see..."

    ```java hl_lines="7 17"
    class RestrictionsTest extends BaseApiConfiguration {

        @Test
        @DisplayName("Should query CPF without restriction")
        void shouldQueryCpfWithoutRestriction() {
            given()
                .spec(SharedRequestSpecs.cpfPathParameter("1234567890"))
            .when()
                .get("/restrictions/{cpf}")
            .then()
                .statusCode(HttpStatus.SC_NOT_FOUND);
        }

        @Test
        void shouldReturnRestriction() {
            given()
                .spec(SharedRequestSpecs.cpfPathParameter("62648716050"))
            .when()
                .get("/restrictions/{cpf}")
            .then()
                .statusCode(HttpStatus.SC_OK)
                .body("message", CoreMatchers.is("CPF 62648716050 has a restriction"));
        }
    }
    ```
    