# REST Assured Basics - Lab 2

In this lab we will learn how to validate the response body.

## 1. Search for a CPF with restriction

### Steps

1. Create a new test method in the  `RestrictionsTest` class named `shouldReturnRestriction()`
2. Add the following in to test:
  - pre-condition (`given()`) using a path parameter `pathParam` using
    - key: `cpf`
    - value: any from the *List of CPF with restrictions*
  - action (`when()`) to get (`get()`) the `/restrictions` endpoint
  - assert (`then()`) in the status code expecting HTTP 200
    - tip: use `HttpStatus.OK`
    - add a `body()` assertion in the response body attribute `message`, using `CoreMatchers.is()` to validate the message

### Expected results

* Green test execution where the following verifications will be performed successfully
  * status code
  * assertion in the `message` attribute  

### 1.1 List of CPF with restrictions

| CPF         |
|-------------|
| 97093236014 |
| 60094146012 |
| 84809766080 |
| 62648716050 |
| 26276298085 |
| 01317496094 |
| 55856777050 |
| 55856777050 |
| 24094592008 |
| 58063164083 |

??? example "Solution"

    ```java
    @Test
    void shouldReturnRestriction() {
        given()
            .pathParam("cpf", "62648716050")
        .when()
            .get("/restrictions/{cpf}")
        .then()
            .statusCode(HttpStatus.SC_OK)
            .body("message", CoreMatchers.is("CPF 62648716050 has a restriction"));
    }   
    ```

## 2. Understand a validation exception

### Steps
1. In the `shouldReturnRestriction()` test, change the message inside the `CoreMatchers.is()` to force a validation error
 - for example: remove the word `restrictions` from the assertion 

### Expected result

* Test will fail, returning the following exception
``` 
java.lang.AssertionError: 1 expectation failed.
JSON path message doesn't match.
Expected: is "CPF 62648716050 has a"
  Actual: CPF 62648716050 has a restriction
```

!!! note "Request and response logged"

    We added, in the `BaseApiConfiguration` a code that will log in the console the request and response when any validation fails.
    You will be able to see the request and response before the exception in the console.
