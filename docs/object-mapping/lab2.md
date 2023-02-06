# Object Mapping - Lab 2

## 1. Update an existing Simulation

### :material-play-box-multiple-outline: Steps

1. In the `SimulationsTest` class, create a test method named `shouldUpdateExistingSimulation()`
2. Create two different data:
    - `String exinstingCpf` with the value as an existing one
    - `Simulation` object with new data, using the builder
3. Add a precondition (`given()`) and
    - add a `pathParameter()` using its value as the existing CPF (the one we need to be able to update)
    - add a `body()` using its value as the simulation with the updated data
    - add the `contentType` related to the body
4. Add the action using the `put()` method to `/simulations/{cpf}`
5. Add the assertion (`then()`) for the:
    - `statusCode` as `200 OK`
    - `body`, as a soft assertion, for each attribute
6. Run the test

!!! tip "Tips"
    * you can use the `Simulation` object to assert the data, as you are updating it
       ```java
       .body("cpf", CoreMatchers.is(simulation.getCpf())
       ```

### :material-checkbox-multiple-outline: Expected results

- Green test execution where the following verifications will be performed successfully
    - status code
    - response body

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    @Test
    void shouldUpdateExistingSimulation() {
        String existingCpf = "17822386034";
        var simulation = Simulation.builder().name("Elias").cpf("17822386034").email("elias@eliasnogueira.com")
                .amount(new BigDecimal("3000.00")).installments(5).insurance(true).build();

        given()
            .pathParam("cpf", existingCpf)
            .body(simulation)
            .contentType(ContentType.JSON)
        .when()
            .put("/simulations/{cpf}")
        .then()
            .statusCode(HttpStatus.SC_OK)
            .body(
                "cpf", CoreMatchers.is(simulation.getCpf()),
                "name", CoreMatchers.is(simulation.getName()),
                "email", CoreMatchers.is(simulation.getEmail()),
                "amount", CoreMatchers.is(simulation.getAmount()),
                "installments", CoreMatchers.is(simulation.getInstallments()),
                "insurance", CoreMatchers.is(simulation.isInsurance())
            );
    }
    ```