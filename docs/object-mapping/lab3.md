# Object Mapping - Lab 3

## 1. Using object deserialization

### :material-play-box-multiple-outline: Steps

1. In the `shouldUpdateExistingSimulation()` remove the `body()` method
2. Add the method `extract().as()`, adding the `Simulation.class` as a parameter for the method `as()`
3. Create an object called `simulationUpdated` and associate it with the `given()` method
    ```java
    var updated  = given()
    ```
4. Add an assertion using the AssertJ library that will verify if the simulation created is equal to the simulation updated
    ```java
    Assertions.assertThat(simulationUpdated).isEqualTo(simulation);
    ```
5. Run the test

### :material-checkbox-multiple-outline: Expected results

- Green test execution where the following verifications will be performed successfully
    - status code
    - response body

!!! info "Info"
    Note that we are verifying two objects using AssertJ.

    When one of the values in an attribute is not equal, AssertJ will show the attribute that does not matches.

    This approach adds an elegant, less code, and modern solution to the assertion.

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    @Test
    void shouldUpdateExistingSimulation() {
        String existingCpf = "17822386034";
        var simulation = Simulation.builder().name("Elias").cpf("17822386034").email("elias@eliasnogueira.com")
                .amount(new BigDecimal("3000.00")).installments(5).insurance(true).build();

        var simulationUpdated =
            given()
                .pathParam("cpf", existingCpf)
                .body(simulation)
                .contentType(ContentType.JSON)
            .when()
                .put("/simulations/{cpf}")
            .then()
                .statusCode(HttpStatus.SC_OK)
                .extract().as(Simulation.class);

        Assertions.assertThat(simulationUpdated).isEqualTo(simulation);
    }
    ```
    