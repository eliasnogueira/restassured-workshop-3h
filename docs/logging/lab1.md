# Logging - Lab 1

## 1. Add the request and response filters to the BaseTest class

### :material-play-box-multiple-outline: Steps

1. Open the `BaseApiConfiguration` class located at `src/test/java` in the `se.jfokus.workshop` package
2. At the end of the method add: 
     - the `RestAssured.filters()` method
     - `new RequestLoggingFilter()` as the first parameter
     - `new ResponseLoggingFilter()` as the second parameter
3. Run the tests

### :material-checkbox-multiple-outline: Expected results

- The test output will show all the requests and responses for each test executed

### :material-check-outline: Solution

??? example "Click to see..."

    ```java hl_lines="14"
    public class BaseApiConfiguration {

        @BeforeAll
        static void mainConfiguration() {
            RestAssured.baseURI = "http://localhost";
            RestAssured.basePath = "/api/v1";
            RestAssured.port= 8088;

            RestAssured.config = RestAssuredConfig.newConfig().
                    jsonConfig(JsonConfig.jsonConfig().numberReturnType(JsonPathConfig.NumberReturnType.BIG_DECIMAL));

            RestAssured.enableLoggingOfRequestAndResponseIfValidationFails();

            RestAssured.filters(new RequestLoggingFilter(), new ResponseLoggingFilter());
        }
    }
    ```