# Object Mapping - Lab 1

## 1. Create the Simulation object

### :material-play-box-multiple-outline: Steps

1. In the `se.jfokus.workshop` package in the `src/main/java` folder, create a package called `models`
2. Create a Java class named `Simulation` in the `se.jfokus.workshop.models` package
3. Add the following annotation on the top of the class name, from Lombok:
    - `@Data`
    - `@Builder`
    - `@NoArgsConstructor`
    - `@AllArgsConstructor`
5. Add the following `private` attributes and it's type:
   
    | type         | name         |
    |--------------|--------------|
    | `String`     | name         |
    | `String`     | cpf          |
    | `String`     | email        |
    | `BigDecimal` | amount       |
    | `int`        | installments |
    | `boolean`    | insurance    |

### :material-checkbox-multiple-outline: Expected results

  - `Simulation` model class created within the correct annotations and attributes

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    package se.jfokus.workshop.models;

    import lombok.AllArgsConstructor;
    import lombok.Builder;
    import lombok.Data;
    import lombok.NoArgsConstructor;

    import java.math.BigDecimal;

    @Data
    @Builder
    @NoArgsConstructor
    @AllArgsConstructor
    public class Simulation {

        private String name;
        private String cpf;
        private String email;
        private BigDecimal amount;
        private int installments;
        private boolean insurance;
    }
    ```

## 2. Create the test for the `POST` request

### :material-play-box-multiple-outline: Steps

1. Open the `SimulationsTest` in `se.jfokus.workshop.simulation` in the `src/test/java` folder
2. Create a test method named `shouldCreateNewSimulation()`
3. Create a `Simulation` object using the builder method
4. Add the precondition using the following methods:
    - `body()`: add the `simulation` object as a parameter
    - `contentType()` add the `ContentType.JSON` from the REST Assured package
5. Add the `post()` request for the `/simulations/` endpoint

!!! tip "Tips"
    * you can use the class name, followed by the `builder()` method, then the methods. Example: `Simulation.builder().`


### :material-checkbox-multiple-outline: Expected results

- Test partially created with the precondition (`given()`) and request (`when()`), without assertions, yet!

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    @Test
    void shouldCreateNewSimulation() {
        var simulation = Simulation.builder().name("Elias").cpf("123456789")
            .email("elias@eliasnogueira.com").amount(new BigDecimal("3000"))
            .installments(5).insurance(true).build();

        given()
            .body(simulation)
            .contentType(ContentType.JSON)
        .when()
            .post("/simulations");
    }
    ```

## 3. Addin the assertion for the `POST` request

### :material-play-box-multiple-outline: Steps

1. In the `shouldCreateNewSimulation()` add the assert action (`then()`):
    - validate the status code as 201 (CREATED)
    - add the `header()` method using:
        - `Location` as the attribute to assert
        - `CoreMatchers.containsString` as the matcher, adding the `CPF` value
2. Run the test

!!! tip "Tips"
    * the code will look like
       ```java
       .then()
          .statusCode(STATUS-CODE-HERE)
          .header("Location", CoreMatchers.containsString(SOMETHING-HERE));
       ```
    * you can get the `CPF` value from the `simulation` object
  
 ### :material-checkbox-multiple-outline: Expected results

 - Green test execution where the following verifications will be performed successfully
    - status code
    - Header

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    @Test
    void shouldCreateNewSimulation() {
        var simulation = Simulation.builder().name("Elias").cpf("123456789").email("elias@eliasnogueira.com")
                .amount(new BigDecimal("3000")).installments(5).insurance(true).build();

        given()
            .body(simulation)
            .contentType(ContentType.JSON)
        .when()
            .post("/simulations/")
        .then()
            .statusCode(HttpStatus.SC_CREATED)
            .header("Location", CoreMatchers.containsString(simulation.getCpf()));
    }
    ```
