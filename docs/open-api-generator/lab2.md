# OpenAPI Generator - Lab 2

## 1. Generate the Client Api

### :material-play-box-multiple-outline: Steps

1. Open the `pom.xml` in the project root folder
2. Go to the `<build> -> <plugins>` section and locate the one within the `openapi-generator-maven-plugin` as `artifactId`
3. After the `<version>` section, add the following code
   ```xml
    <executions>
        <execution>
            <id>generate-client-api-code</id>
            <goals>
                <goal>generate</goal>
            </goals>
            <phase>generate-sources</phase>
            <configuration>
                <inputSpec>
                    ${project.build.directory}/openapiSpecs/credit-api.yaml
                </inputSpec>
                <invokerPackage>com.eliasnogueira.credit.invoker</invokerPackage>
                <apiPackage>com.eliasnogueira.credit.api</apiPackage>
                <modelPackage>eliasnogueira.credit.model</modelPackage>
                <generatorName>java</generatorName>
                <generateApiTests>false</generateApiTests>
                <generateModelTests>false</generateModelTests>
                <configOptions>
                    <library>rest-assured</library>
                    <serializationLibrary>jackson</serializationLibrary>
                </configOptions>
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
- You will see the following log related to the `openapi-generator-maven-plugin`
  ```
   [INFO] --- openapi-generator-maven-plugin:6.2.1:generate (generate-client-api-code) @ credit-api-tests ---
   [INFO] Generating with dryRun=false
   [INFO] Output directory (YOUR_DIR/credit-api-tests/target/generated-sources/openapi) does not exist, or is inaccessible. No file (.openapi-generator-ignore) will be evaluated.
   [INFO] OpenAPI Generator: java (client)
   [INFO] Generator 'java' is considered stable.
   [INFO] Environment variable JAVA_POST_PROCESS_FILE not defined so the Java code may not be properly formatted. To define it, try 'export JAVA_POST_PROCESS_FILE="/usr/local/bin/clang-format -i"' (Linux/Mac)
   [INFO] NOTE: To enable file post-processing, 'enablePostProcessFile' must be set to `true` (--enable-post-process-file for CLI).
   [INFO] Processing operation OPERATION
   [INFO] writing file FILE
  ```
- The Client Api and Model classes will be created in the following structure
  ```
  └── target/
    └── generated-resources/
        └── openapi/
            └── src/
                └── main/
                    └── java/
                        └── com/
                            └── eliasnogueira/
                                └── credit/
                                    ├── api/
                                    │   └── *.java
                                    └── model/
                                        └── *.java
  ```

### :material-plus-box: Additional post-step

1. Open the `target` folder
2. Right-click the `generated-sources` folder
3. Select `Mark directory as -> Generated Sources Root`

!!! note "Why we do have the additional post-step?"
    The `openapi-generator-maven-plugin` is generating a Java project in the `target/generated-sources` directory.
    We need to tell the IDE to consider that folder as "sources" inferring that we will use the code inside it in the project.
