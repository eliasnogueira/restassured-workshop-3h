# REST Assured Basics - Lab 4

## 1. Deleting a simulation

### :material-play-box-multiple-outline: Steps

1. In the `SimulationsTest` class, create a test method named `shouldDeleteExistingSimulation()`
2. Add a precondition (`given()`) and set the CPF to delete using the `pathParameter()` method
3. Add the action using the `delete()` method to `/simulations/{cpf}`
4. Add the assertion (`then()`) in the `statusCode` as `204 no content`
5. Run the test

### :material-checkbox-multiple-outline: Expected results

- Green test execution where the following verifications will be performed successfully
    - status code

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    @Test
    void shouldDeleteExistingSimulation() {
        given()
            .pathParam("cpf", "66414919004")
        .when()
            .delete("/simulations/{cpf}")
        .then()
            .statusCode(HttpStatus.SC_NO_CONTENT);
    }
    ```