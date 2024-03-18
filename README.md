# Spring Boot With OpenAPI Generator
This repo is for testing OpenAPI Generator in Spring Boot. OpenAPI Specification and plugins are used to define endpoints and config to generate automatic code.

## Usage (Maven)
Add to your `build->plugins` section (default phase is `generate-sources` phase)

```xml
<!-- OpenAPI Generator Plugin -->
<plugin>
    <groupId>org.openapitools</groupId>
    <artifactId>openapi-generator-maven-plugin</artifactId>
    <!-- RELEASE_VERSION -->
    <version>7.4.0</version>
    <!-- /RELEASE_VERSION -->
    <executions>
        <execution>
            <goals>
                <goal>generate</goal>
            </goals>
            <configuration>
                <inputSpec>${project.basedir}/src/main/resources/api/openapi.yaml</inputSpec>
                <generatorName>spring</generatorName>
                <ignoreFileOverride>${project.basedir}/src/main/resources/api/.openapi-generator-ignore</ignoreFileOverride>
                <configurationFile>${project.basedir}/src/main/resources/api/config.json</configurationFile>
            </configuration>
        </execution>
    </executions>
</plugin>
```

Add the `config.json` file to the path you specified in the plugin configuration (`configurationFile`).

```json
{
  "library": "spring-boot",
  "dateLibrary": "java21",
  "useSpringBoot3": "true",
  "hideGenerationTimestamp": true,
  "sourceFolder": "src/gen/java/main",
  "modelPackage": "api.model",
  "apiPackage": "api",
  "invokerPackage": "api",
  "serializableModel": true,
  "useTags": true,
  "useGzipFeature" : true,
  "hateoas": true,
  "withXml": true,
  "importMappings": {
    "ResourceSupport":"org.springframework.hateoas.RepresentationModel",
    "Link": "org.springframework.hateoas.Link"
  }
}
```

Add the `.openapi-generator-ignore` file to a path specified in the plugin configuration (`ignoreFileOverride`).
```.openapi generator
**/*Controller.java
```

## Generate Code
Enter the following command in your terminal to run the plugin as a stage of the build and generate the code:

```shell
mvn clean compile
```

## Result
After finishing the above command, the generated code is placed in `target/generated-sources/openapi/src/gen/java/main/api` path.

You can change the generated code path in `config.json`.

## References
[OpenAPI Specification](https://swagger.io/specification/)

[OpenAPI Generator Maven Plugin](https://github.com/OpenAPITools/openapi-generator/blob/master/modules/openapi-generator-maven-plugin/README.md)

[OpenAPI Generator Spring Github](https://github.com/OpenAPITools/openapi-generator/blob/master/docs/generators/spring.md)

[OpenAPI Generator Spring Docs](https://openapi-generator.tech/docs/generators/spring/)

[Modern API Development with Spring and Spring Boot (2021)](https://github.com/PacktPublishing/Modern-API-Development-with-Spring-and-Spring-Boot)