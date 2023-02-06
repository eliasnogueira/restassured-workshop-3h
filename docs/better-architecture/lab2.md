# Better architecture - Lab 2

## 1. Changing the  `RestrictionsTest` - `shouldQueryCpfWithoutRestriction()` test

1. Open the `RestrictionsTest` located in the `se.jfokus.workshop.restriction` package in the `src/test/java` folder
2. Remove the inheritance of the `BaseApiConfiguration`
3. Comment the current code created in the `shouldQueryCpfWithoutRestriction()` test
4. Create a `RestrictionsApiService` within the name `restrictionsService`
5. Call the method `restrictionsService.queryCpf()`, using any CPF (without a restriction)
6. Associate its response to a boolean
7. Add an assertion using the `isTrue()` method from AssertJ
8. Run the test

### :material-checkbox-multiple-outline: Expected results

- Green test execution

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    @Test
    void shouldQueryCpfWithoutRestriction() {
        RestrictionsApiService restrictionsServices = new RestrictionsApiService();

        boolean isDeleted = restrictionsServices.queryCpf("1234567890");
        Assertions.assertThat(isDeleted).isTrue();
    }  
    ```

## 2. Changing the  `RestrictionsTest` - `shouldReturnRestriction()` test

1. In the `RestrictionsTest`, comment the current code created in the `shouldReturnRestriction()` test
2. Create a `RestrictionsApiService` within the name `restrictionsService`
3. Call the method `restrictionsService.queryCpfWithRestriction()`, using any CPF (without a restriction)
4. Associate its response to the `MessageV1` class from `com.eliasnogueira.credit.model` package (auto-generated from the OpenAPI spec)
5. Add an assertion using the `contains()` method from AssertJ, where it's necessary to use the `getMessage()` method from the `MessageV1` return
6. Run the test

### :material-checkbox-multiple-outline: Expected results

- Green test execution where the following verifications will be performed successfully

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    @Test
    void shouldReturnRestriction() {
        RestrictionsApiService restrictionsApiService = new RestrictionsApiService();
        MessageV1 message = restrictionsApiService.queryCpfWithRestriction("60094146012");

        Assertions.assertThat(message.getMessage()).contains("60094146012");
    }
    ```

!!! tip "Tip"
    You can remove the duplication of the `RestrictionsApiService` adding it as a private global variable in the test.

     ```java hl_lines="3"
     class RestrictionsTest extends BaseApiConfiguration {

         private RestrictionsApiService restrictionsServices = new RestrictionsApiService();

         @Test
         void shouldQueryCpfWithoutRestriction() {
             // code
         }

         @Test
         void shouldReturnRestriction() {
             // code
         }
     }
     ```


## 3. Cleaning up `BaseApiConfiguration` class

1. Open the `BaseApiConfiguration` located in the `se.jfokus.workshop` package in the `src/test/java` folder
2. Remove the usage of:
    - `RestAssured.baseURI = "http://localhost";`
    - `RestAssured.basePath = "/api/v1";`
    - `RestAssured.port= 8088;`
3. Add (again) the inheritance of the `BaseApiConfiguration` to the `RestrictionsTest`
4. Run the tests

### :material-checkbox-multiple-outline: Expected results

- Green test execution where the following verifications will be performed successfully
- All the request and response logs showing in the console

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    class RestrictionsTest extends BaseApiConfiguration {

        private RestrictionsApiService restrictionsServices = new RestrictionsApiService();

        @Test
        void shouldQueryCpfWithoutRestriction() {
            boolean isDeleted = restrictionsServices.queryCpf("1234567890");
            Assertions.assertThat(isDeleted).isTrue();
        }

        @Test
        void shouldReturnRestriction() {
            MessageV1 message = restrictionsServices.queryCpfWithRestriction("60094146012");
            Assertions.assertThat(message.getMessage()).contains("60094146012");
        }
    }
    ```
