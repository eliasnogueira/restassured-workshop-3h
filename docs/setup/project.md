# Setup - Project

The setup consists in creating the test project. You can donwload it or create one using the necessary libraries.

## 1. Clone or Download the base project

The base project already have all the libraries added.

### 1.1 Clone the project

1. Open your Terminal
2. Navigate to a know folder in your computer
3. Run the following command to clone the project
   ```
   git clone https://github.com/eliasnogueira/restassured-workshop-3h-test.git
   ```

### 1.2 [optional] Download

1. Click in the following link to download the project as a zip file
  - https://github.com/eliasnogueira/restassured-workshop-3h-test/archive/refs/heads/main.zip


## 2. Create a new project

!!! note "This is an optional step if you need to create the project yourself!"

1. Open your preferred IDE
2. Create a new Java project:
- based on Maven
- named `credit-api-tests`
- you can name any group, but I recommend you using `com.workshop`

### 2.1 Adding the libraries

We need to add the base dependencies to start creating the tests.

1. Open the `pom.xml` file
2. Add the `properties` section
```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.target>17</maven.compiler.target>
    <maven.compiler.source>17</maven.compiler.source>

    <maven-compiler-plugin.version>3.10.1</maven-compiler-plugin.version>
    <wagon-maven-plugin.version>2.0.2</wagon-maven-plugin.version>
    <openapi-generator-maven-plugin.version>6.2.1</openapi-generator-maven-plugin.version>

    <junit.version>5.9.2</junit.version>
    <rest-assured.version>5.3.0</rest-assured.version>
    <assertj-core.version>3.24.2</assertj-core.version>
    <datafaker.version>1.7.0</datafaker.version>
    <lombok.version>1.18.24</lombok.version>
    <jackson-databind.version>2.14.1</jackson-databind.version>
    <swagger-annotations.version>1.6.6</swagger-annotations.version>
    <javax.annotation-api>1.3.2</javax.annotation-api>
    <jsr305.version>3.0.2</jsr305.version>
    <jackson-datatype-jsr310.version>2.14.1</jackson-datatype-jsr310.version>
    <jackson-databind-nullable.version>0.2.4</jackson-databind-nullable.version>
</properties>
```
2. Now add the `dependencies` section
```xml
<dependencies>

    <!-- Testing libraries -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>${junit.version}</version>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>io.rest-assured</groupId>
        <artifactId>rest-assured</artifactId>
        <version>${rest-assured.version}</version>
    </dependency>

    <dependency>
        <groupId>org.assertj</groupId>
        <artifactId>assertj-core</artifactId>
        <version>${assertj-core.version}</version>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>net.datafaker</groupId>
        <artifactId>datafaker</artifactId>
        <version>${datafaker.version}</version>
        <scope>test</scope>
    </dependency>

    <!-- Runtime libraries -->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>${lombok.version}</version>
        <scope>provided</scope>
    </dependency>

    <!-- OpenAPI generation libraries -->
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>${jackson-databind.version}</version>
    </dependency>

    <dependency>
        <groupId>io.swagger</groupId>
        <artifactId>swagger-annotations</artifactId>
        <version>${swagger-annotations.version}</version>
    </dependency>

    <dependency>
        <groupId>javax.annotation</groupId>
        <artifactId>javax.annotation-api</artifactId>
        <version>${javax.annotation-api}</version>
    </dependency>

    <dependency>
        <groupId>com.google.code.findbugs</groupId>
        <artifactId>jsr305</artifactId>
        <version>${jsr305.version}</version>
    </dependency>

    <dependency>
        <groupId>com.fasterxml.jackson.datatype</groupId>
        <artifactId>jackson-datatype-jsr310</artifactId>
        <version>${jackson-datatype-jsr310.version}</version>
    </dependency>

    <dependency>
        <groupId>org.openapitools</groupId>
        <artifactId>jackson-databind-nullable</artifactId>
        <version>${jackson-databind-nullable.version}</version>
    </dependency>

</dependencies>
```
3. Finally, add the `build` section
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>${maven-compiler-plugin.version}</version>
            <configuration>
                <source>${maven.compiler.source}</source>
                <target>${maven.compiler.target}</target>
            </configuration>
        </plugin>

        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>wagon-maven-plugin</artifactId>
            <version>${wagon-maven-plugin.version}</version>
        </plugin>

        <plugin>
            <groupId>org.openapitools</groupId>
            <artifactId>openapi-generator-maven-plugin</artifactId>
            <version>${openapi-generator-maven-plugin.version}</version>
        </plugin>
    </plugins>
</build>
```

### 2.2 Make sure you have the following project structure

You must have the following structure in your project:
```
─── src
├── main
│   └── java
│       └── com.workshop
└── test
│   └──java
│       └── com.workshop
└───── resources
```

## 3. Done!
