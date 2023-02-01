# Better architecture Lab 1

## 1. Create the `RestApiClientBuilder` class

### :material-play-box-multiple-outline: Steps

1. In the `se.jfokus.workshop` package create a Java class named `RestApiClientBuilder` 
2. Add the following code inside it
    ```java
    import io.restassured.builder.RequestSpecBuilder;

    import java.util.function.Function;
    import java.util.function.Supplier;

    public class RestApiClientBuilder {

        public <T> T build(Function<Supplier<RequestSpecBuilder>, T> clientCreator) {
            Supplier<RequestSpecBuilder> requestSpecBuilderSupplier = () -> new RequestSpecBuilder()
                    .addRequestSpecification(
                            new RequestSpecBuilder()
                                    .setBaseUri("http://localhost")
                                    .setPort(8088)
                                    .build());

            return clientCreator.apply(requestSpecBuilderSupplier);
        }
    }
    ```

### :material-checkbox-multiple-outline: Expected results

  - `RestApiClientBuilder` class created... don't panic, we will use it later!

## 2. Create the `RestrictionApiClient` class

### :material-play-box-multiple-outline: Steps

1. In the `se.jfokus.workshop` package in the `src/main/java` folder, create a package called `api.client`
2. Create a Java class named `RestrictionsApiClient` in the `se.jfokus.workshop.api.client` package
3. Add the following code inside it
    ```java
    import com.eliasnogueira.credit.api.RestrictionsApi;
    import io.restassured.response.Response;
    import se.jfokus.workshop.api.RestApiClientBuilder;

    import java.util.function.Function;

    public class RestrictionsApiClient {

        private RestrictionsApi restrictionsApi = new RestApiClientBuilder().build(RestrictionsApi::restrictions);

        public Response queryCpf(String cpf) {
            return restrictionsApi.oneUsingGET().cpfPath(cpf).execute(Function.identity());
        }
    }
    ```

### :material-checkbox-multiple-outline: Expected results

  - `RestrictionsApiClient` class created... don't panic, we will use it later!


## 3. Create the `RestrictionApiService` class

### :material-play-box-multiple-outline: Steps

1. In the `se.jfokus.workshop` package in the `src/main/java` folder, create a package called `api.service`
2. Create a Java class named `RestrictionsApiService` in the `se.jfokus.workshop.api.service` package
3. Add the following code inside it
    ```java
    import com.eliasnogueira.credit.model.MessageV1;
    import org.apache.http.HttpStatus;
    import se.jfokus.workshop.api.client.RestrictionsApiClient;

    public class RestrictionsApiService {

        private RestrictionsApiClient restrictionsApiClient = new RestrictionsApiClient();

        /**
        * Query CPF without a restriction
        */
        public boolean queryCpf(String cpf) {
            restrictionsApiClient.queryCpf(cpf).then().statusCode(HttpStatus.SC_NOT_FOUND);
            return true;
        }

        public MessageV1 queryCpfWithRestriction(String cpf) {
            return restrictionsApiClient.queryCpf(cpf).then().
                    statusCode(HttpStatus.SC_OK).extract().as(MessageV1.class);
        }

    }
    ```

### :material-checkbox-multiple-outline: Expected results

  - `RestrictionsApiService` class created... don't panic, we will use it later!