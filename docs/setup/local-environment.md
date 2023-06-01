# Setup - Local environment

The first thing we need to do is to check the setup and download the necessary project to run the tests.

## 1. Check your machine

- [ ] JDK 17 + installed
- [ ] Modern IDE (Intellij, VSCode, etc...)
- [ ] Git


## 2. Using the backend project

The backend project was created using SpringBoot 3 and an in-memory database. You access it at [https://github.com/eliasnogueira/credit-api](https://github.com/eliasnogueira/credit-api).

You can use {==one of the following approaches==} to use the application:

### :fontawesome-solid-jar: JAR file

1. Open the project package session on GitHub: [https://github.com/eliasnogueira/credit-api/packages/1742648](https://github.com/eliasnogueira/credit-api/packages/1742648)
2. In the *Assets* session, download the `.jar` file
3. Open the Terminal and navigate to the folder the file was saved
```
cd Downloads
```
4. Start the application by running the following:
```
java -jar file-name.jar
```

### :material-github: Direct project usage

1. Clone the backend project running one of the following cloning methods:

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

2. Open the Terminal and navigate to the project directory
3. Run the application
```
./mvnw spring-boot:run
```

!!! note "Running inside the IDE"

You can also run the `CreditApiApplication` class located at `src/main/java`


## 3. Access the OpenAPI specification
We will know a little bit more about the API using the OpenAPI specification as it will also be the entry point to run exploratory checks before the test automation.


* Clone the backend project by running one of the following cloning methods:

=== ":simple-openapiinitiative: Open API page"
[http://localhost:8088/swagger-ui/index.html](http://localhost:8088/swagger-ui/index.html)
