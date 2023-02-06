# Extra - Lab 2

In thi lab you need to refactor the `SimulationsTest` placed in the `se.jfokus.workshop.simulation` in the `src/java/test` folder.
A beter approach is to comment all the previous tests.


## 1. Refactor the `shouldRetrieveAllSimulations()` test

### Precondition

1. Create a global attribute instance for the `SimulationsApiService`
    ```java
    private final SimulationsApiService simulationsApiService = new SimulationsApiService();
    ```

### :material-play-box-multiple-outline: Steps

1. In the `shouldRetrieveAllSimulations()` test, use the `SimulationsApiService` to:
    - retrieve all the simulations
    - assert if the list size is equals to or higher than 1
2. Run the test

!!! tip "Tips"
    To verify the returned list size you can use the following matcher from AssertJ:
    ```java
    Assertions.assertThat(simulations).hasSizeGreaterThanOrEqualTo(1);
    ```

### :material-checkbox-multiple-outline: Expected results

- Green test execution

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    @Test
    void shouldRetrieveAllSimulations() {
        var simulations = simulationsApiService.retrieveSimulations();
        Assertions.assertThat(simulations).hasSizeGreaterThanOrEqualTo(1);
    }    
    ```


## 2. Create a test to find a simulation by name

### :material-play-box-multiple-outline: Steps

1. Create a new test method called `shouldRetrieveSimulationByItsName()`
2. Use the method, from the service class, which is expecting the name as a query parameter
3. Assert only the name returned and for this use the following code
   ```java
   Assertions.assertThat(simulations).anySatisfy(
        simulation -> Assertions.assertThat(simulation.getName()).isEqualTo("Tom"));
   ```
4. Run the test

!!! tip "Tips"
    To verify the returned list size you can use the following matcher from AssertJ:
    ```java
    Assertions.assertThat(simulations).hasSizeGreaterThanOrEqualTo(1);
    ```

### :material-checkbox-multiple-outline: Expected results

- Green test execution

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    @Test
    void shouldRetrieveSimulationByItsName() {
        var simulations = simulationsApiService.retrieveSimulations("Tom");

        Assertions.assertThat(simulations).anySatisfy(
                simulation -> Assertions.assertThat(simulation.getName()).isEqualTo("Tom"));
    }   
    ```

## 3. Create a test to find a simulation by cpf

### :material-play-box-multiple-outline: Steps

1. Create a new test method called `shouldFindSimulationByCpf()`
2. Use the method, from the service class, which is expecting the `cpf` as path parameter
3. Assert all the data, including the `id`, using the following code snippet
   ```java
   SoftAssertions.assertSoftly(softly -> {
      Assertions.assertThat(simulation.getSomething()).assertMethod();
      // similar line for the other attributes
   });
   ```
4. Run the test
   
!!! abstract "Soft assertions"
    AssertJ has a feature called [Soft Assertions](https://joel-costigliola.github.io/assertj/assertj-core-features-highlight.html#soft-assertions)
    It will assert all data inside the `assertSoftly` method, not stopping the execution when the assertion fails.

!!! tip "Tips"
    Use the following assertions methods to replace the `assertMethod()` in step 3:
    
    * `isNotNull()` for the `id` assertion
    * `isEqualTo()` for all text assertions
    * `isTrue()` or `isFalse()` for the boolean assertion

### :material-checkbox-multiple-outline: Expected results

- Green test execution

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    @Test
    void shouldFindSimulationByCpf() {
        var simulation = simulationsApiService.retrieveSimulation("66414919004");
        SoftAssertions.assertSoftly(softly -> {
            Assertions.assertThat(simulation.getId()).isNotNull();
            Assertions.assertThat(simulation.getName()).isEqualTo("Tom");
            Assertions.assertThat(simulation.getCpf()).isEqualTo("66414919004");
            Assertions.assertThat(simulation.getEmail()).isEqualTo("tom@gmail.com");
            Assertions.assertThat(simulation.getAmount()).isEqualTo("11000.00");
            Assertions.assertThat(simulation.getInstallments()).isEqualTo(3);
            Assertions.assertThat(simulation.isInsurance()).isTrue();
        });
    }  
    ```

## 4. Create a test to create a new simulation

### :material-play-box-multiple-outline: Steps

1. Create a new test method called `shouldCreateSimulation()`
2. Create a `Simulation` object to use as the request body, with any data you like inside
3. Assert the return, which is a `Header` using the `getValue()` and the `contains()` assertion to see if the cpf is present in the location
   ```java
   Assertions.assertThat(header.getValue()).contains(simulation.getCpf());
   ```
4. Run the test

### :material-checkbox-multiple-outline: Expected results

- Green test execution

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    @Test
    void shouldCreateSimulation() {
        var simulation = Simulation.builder().name("Robert").cpf("98765432103").email("robert@gmail.com")
                .amount(new BigDecimal("3000.00")).installments(5).insurance(true).build();

        var header = simulationsApiService.createSimulation(simulation);
        Assertions.assertThat(header.getValue()).contains(simulation.getCpf());
    }
    ```

## 5. Create a test to update an existing simulation

### :material-play-box-multiple-outline: Steps

1. Create a new test method called `shouldUpdateExistingSimulation()`
2. Create a `Simulation` object to use as the request body, with any data you like inside
3. Create the simulation using the `createSimulation()` method from the service class
4. Change the name of the Simulation created in step 2
5. Update the Simulation using the `cpf` from the object created in step 2
6. Assert that the Simulation object from the step 2 is equal to the one returned from the updated in the step 5
7. Run the test

### :material-checkbox-multiple-outline: Expected results

- Green test execution

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    @Test
    void shouldUpdateExistingSimulation() {
        var newSimulation = Simulation.builder().name("Robert").cpf("748392749450").email("robert@gmail.com")
                .amount(new BigDecimal("3000.00")).installments(5).insurance(true).build();
        simulationsApiService.createSimulation(newSimulation);

        newSimulation.setName("Different name");

        var simulationUpdated = simulationsApiService.updateSimulation(newSimulation.getCpf(), newSimulation);
        Assertions.assertThat(simulationUpdated).isEqualTo(newSimulation);
    }
    ```

## 6. Create a test to delete an existing simulation

### :material-play-box-multiple-outline: Steps

1. Create a new test method called `shouldDeleteExistingSimulation()`
2. Create a `Simulation` object to use as the request body, with any data you like inside
3. Create the simulation using the `createSimulation()` method from the service class
4. Delete the simulation created using the delete method from the service class, using the cpf from the simulation created
5. Assert that the return is `true`

### :material-checkbox-multiple-outline: Expected results

- Green test execution

### :material-check-outline: Solution

??? example "Click to see..."

    ```java
    @Test
    void shouldDeleteExistingSimulation() {
        var simulation = Simulation.builder().name("Robert").cpf("874222357").email("robert@gmail.com")
                .amount(new BigDecimal("3000.00")).installments(5).insurance(true).build();
        simulationsApiService.createSimulation(simulation);

        var isDeleted = simulationsApiService.deleteSimulation(simulation.getCpf());
        Assertions.assertThat(isDeleted).isTrue();
    }
    ```
