# Data - Lab 1

## 1. Create the `SimulationDataFactory` class

### :material-play-box-multiple-outline: Steps

1. Open the `pom.xml` and remove the `<scope>test</scope>` for the DataFaker library
2. In the `se.jfokus.workshop` package create package called `data` in the `src/main/java` 
3. Create a class called `SimulationDataFactory` in the `se.jfokus.workshop` in the `src/main/java`
4. Do the following in the class
    - make the class `final`
    - create a private constructuor
5. Add the `Faker` object as a global attribute
    ```java
    private static Faker faker = new Faker();
    ```
6. Add the following code inside it
    ```java
    public Simulation validSimulation() {

        return Simulation.builder().
                cpf(faker.number().digits(11)).
                name(faker.name().fullName()).
                email(faker.internet().emailAddress()).
                amount(new BigDecimal(faker.number().numberBetween(100, 40000))).
                installments(faker.number().numberBetween(2, 48)).
                insurance(faker.bool().bool())
            .build();
    }
    ```
7. Open the `SimulationsTest` class
8. In the `shouldCreateNewSimulation()` and replace the simulation object by the usage of the `SimulationDataFactory.validSimulation()`
9.  Run the test

### :material-checkbox-multiple-outline: Expected results

- Green test execution

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    class SimulationsTest extends BaseApiConfiguration {

        @Test
        void shouldCreateNewSimulation() {
            var simulation = SimulationDataFactory.validSimulation();

            given()
                .body(simulation)
                .contentType(ContentType.JSON)
            .when()
                .post("/simulations/")
            .then()
                .statusCode(HttpStatus.SC_CREATED)
                .header("Location", CoreMatchers.containsString(simulation.getCpf()));
        }
    }
    ```
