# OpenAPI Generator - Lab 1

## 1. Download the spec from the project

### :material-play-box-multiple-outline: Steps

1. Open the `pom.xml` in the project root folder
2. Go to the `<build> -> <plugins>` section and locate the one within the `wagon-maven-plugin` as `artifactId`
3. After the `<version>` section, add the following code
   ```xml
    <executions>
        <execution>
            <id>download-credit-api-spec</id>
            <goals>
                <goal>download-single</goal>
            </goals>
            <phase>generate-sources</phase>
            <configuration>
                <url>https://raw.githubusercontent.com/eliasnogueira/credit-api/main/src/main/resources/static/credit-api.yaml</url>
                <toDir>${project.basedir}/target/openapiSpecs</toDir>
            </configuration>
        </execution>
    </executions>
   ```
4. Execute the following command in the Terminal
   ```
   mvn compile
   ```


### :material-checkbox-multiple-outline: Expected results

- The build will be successful
- You will see the following log related to the `wagon-maven-plugin`
  ```
   [INFO] --- wagon-maven-plugin:2.0.2:download-single (download-credit-api-spec) @ credit-api-tests ---
   [INFO] Downloading: https://raw.githubusercontent.com/eliasnogueira/credit-api/main/src/main/resources/static/credit-api.yaml to YOUR_COMPUTER_PATH/credit-api-tests/target/openapiSpecs/credit-api.yaml
  ```
- The `credit-api.yaml` file will be placed in the `target/openapiSpecs` folder
