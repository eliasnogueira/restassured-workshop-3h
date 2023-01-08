# Setup

The first thing we need to do is to check the setup and download the necessary project to run the tests.

## 1. Check your machine

- [ ] JDK 17 + installed
- [ ] Modern IDE (Intellij, VSCode, etc...)
- [ ] Git


## 2. Clone the backend project

* Clone the backend project runing one of the following cloning methods:

    === "HTTPS"
        ```
        git clone https://github.com/eliasnogueira/credit-api.git
        ```

    === "SSH"
        ```
        git clone git@github.com:eliasnogueira/credit-api.git
        ```

    === "GitHub CLI"
        ```
        gh repo clone eliasnogueira/credit-api
        ```

    === "Download ZIP"
        [https://github.com/eliasnogueira/credit-api/archive/refs/heads/main.zip](https://github.com/eliasnogueira/credit-api/archive/refs/heads/main.zip)

* Open the `credit-api` project using your preferred IDE
* Run MAven Package to download the dependent libraries
  ```
  mvn package
  ```

## 3. Run the application
Run the following command in your Terminal, which will run the application at the `localhost` using the `8088` port by default.

```
mvn spring-boot:run
```

!!! note "Running locally"

    You can also simply run the `CreditApiApplication` class located at `src/main/java`


## 4. Access the OpenAPI specification
We will know a little bit more about the API using the OpenAPI specification as it will also be the entry point to run exploratory checks before the test automation.


* Clone the backend project runing one of the following cloning methods:

    === ":simple-openapiinitiative: Open API page"
        [http://localhost:8088/swagger-ui/index.html](http://localhost:8088/swagger-ui/index.html)
