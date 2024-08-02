---
id: getting-started
title: Getting started
description: "Leverage Zeebe APIs (gRPC and REST) in your Spring Boot project."
---

* Zeebe APIs | Spring Boot project
  * [gRPC](/apis-tools/zeebe-api/grpc.md) and 
  * [REST](/apis-tools/zeebe-api-rest/zeebe-api-rest-overview.md)
* Camunda Spring SDK
  * == expansion of Spring Zeebe SDK / -- interact with -- ALL Camunda APIs | Java Spring

## Version compatibility

| Camunda Spring SDK version | JDK    | Camunda version | Bundled Spring Boot version |
| -------------------------- | ------ | --------------- | --------------------------- |
| 8.5.x                      | \>= 17 | 8.5.x           | 3.2.x                       |

## Add the Spring Zeebe SDK to your project

* add 

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
        </releases>
        <snapshots>
            <enabled>false</enabled>
        </snapshots>
        <id>identity</id>
        <name>Camunda Identity</name>
        <url>https://artifacts.camunda.com/artifactory/camunda-identity/</url>
    </repository>
</repositories>
```

```xml
<dependency>
    <groupId>io.camunda</groupId>
    <artifactId>spring-boot-starter-camunda-sdk</artifactId>
    <version>8.5.0</version>
</dependency>
```

## Enable the Java Compiler `-parameters`-flag

* 👁️If you do NOT want to specify annotation values (_Example:_ process variable name | [variable](#using-variable) annotation) -> required the Java compiler flag `-parameters` 👁️	
* via
  * Mavem

    ```xml
    <build>
        <plugins>
          <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
              <compilerArgs>
                <arg>-parameters</arg>
              </compilerArgs>
            </configuration>
          </plugin>
        </plugins>
      </build>
    ```
    * Gradle

    ```xml
    tasks.withType(JavaCompile) {
        options.compilerArgs << '-parameters'
    }
    ```

    * IntelliJ

    ```agsl
    Settings > Build, Execution, Deployment > Compiler > Java Compiler
    ```

## Configuring the Camunda 8 connection

* `camunda.client.mode`
  * -- based on -- Camunda types
    * Saas
    * Self-Managed
* Zeebe configured via URL
  * _Example:_ "http://localhost:26500"
  * NOT via `localhost:26500` + plaintext connection flag 

### Saas

* `camunda.client.mode:Saas`
* _Example:_ "src/main/resources/application.yaml"

    ```yaml
    camunda:
      client:
        mode: saas
        auth:
          client-id: <your client id>
          client-secret: <your client secret>
        cluster-id: <your cluster id>
        region: <your cluster region>
    ```

### Self-Managed

* `camunda.client.mode:self-managed`
* if you set up a Self-Managed cluster + Identity
  * Keycloak -- is used as the -- default Identity provider
  * _Example:_ default port config (from Docker Compose or port-forward with Helm charts) -> configure the accompanying Spring profile and client credentials

    ```yaml
    camunda:
      client:
        mode: self-managed
        auth:
          client-id: <your client id>
          client-secret: <your client secret>
          issuer: http://localhost:18080/auth/realms/camunda-platform/protocol/openid-connect/token
    ```

* if you have different endpoints / your applications OR want to disable a client

    ```yaml
    camunda:
      client:
        mode: self-managed
        tenant-ids:
          - <default>
        auth:
          client-id: <your client id>
          client-secret: <your client secret>
          issuer: http://localhost:18080/auth/realms/camunda-platform/protocol/openid-connect/token
        zeebe:
          enabled: true
          grpc-address: http://localhost:26500
          rest-address: http://localhost:8080
          prefer-rest-over-grpc: false
          audience: zeebe-api
    ```

## Obtain the Zeebe client

* inject the Zeebe client
* uses
  * create new workflow instances

```java
@Autowired
private ZeebeClient client;
```

## Deploy process models

* `@Deployment` 
  * -- based on -- [the Spring resource loader](#resources-resourceloader) mechanism
  * _Example:_

    ```java
    @SpringBootApplication
    @Deployment(resources = "classpath:demoProcess.bpmn")
    public class MySpringBootApplication {
    ```

  * _Example:_ deploy multiple files | at once

    ```java
    @Deployment(resources = {"classpath:demoProcess.bpmn" , "classpath:demoProcess2.bpmn"})
    ```

  * _Example:_ define wildcard patterns

    ```java
    @Deployment(resources = "classpath*:/bpmn/**/*.bpmn")
    ```

## Implement the job worker

* [the configuration documentation](/apis-tools/spring-zeebe-sdk/configuration.md) 
```java
@JobWorker(type = "foo")
public void handleJobFoo(final ActivatedJob job) {
  // do whatever you need to do
}
```

 
