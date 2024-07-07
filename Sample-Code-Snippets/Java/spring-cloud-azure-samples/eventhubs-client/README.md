
# Sending and Receiving Message by Azure Event Hubs and Autoconfigured SDK Client in Spring Boot Application


>The project is copied and adapted from [    azure-spring-boot-samples/eventhubs/spring-cloud-azure-stream-binder-eventhubs/eventhubs-binder](https://github.com/Azure-Samples/azure-spring-boot-samples/tree/8a6ccc248fd6c61f3bec4470eb453238fe77bfd5/eventhubs/spring-cloud-azure-stream-binder-eventhubs/eventhubs-binder)


This code sample demonstrates how to use the client of `Azure Event Hubs SDK` to interact with `Azure Event Hubs`.

## What You Will Build

You will build an application that uses `spring-cloud-azure-starter-eventhubs` to send and receive messages with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).

## What You Need

- Running Azure Event Hubs Emulator
- Running Nginx Reverse Proxy
- Absolute path to the generated keystore.jks file
- [JDK8](https://www.oracle.com/java/technologies/downloads/) or later
- Maven
- You can also import the code straight into your IDE:
    - [IntelliJ IDEA](https://www.jetbrains.com/idea/download)


## Run Locally

Run with JVM arguments:
- `-Djavax.net.ssl.trustStore=ABS_PATH/keystore.jks`
- `-Djavax.net.ssl.trustStorePassword=changeit`
- `-Djavax.net.ssl.trustStoreType=jks`

Replace ABS_PATH with the absolute path to the generated keystor.jks file. (on Windows use `c:/path/to/keystore`)

### Run the sample with Maven

In your terminal, run:

```shell
mvn clean spring-boot:run -Dspring-boot.run.jvmArguments="-Djavax.net.ssl.trustStore=ABS_PATH/keystore.jks -Djavax.net.ssl.trustStorePassword=changeit -Djavax.net.ssl.trustStoreType=jks"
```

### Run the sample in IDEs

You can debug your sample by adding the saved output values to the tool's environment variables or the sample's `application.yaml` file.

* If your tool is `IDEA`, please refer to [Debug your first Java application](https://www.jetbrains.com/help/idea/debugging-your-first-java-application.html) and [add environment variables](https://www.jetbrains.com/help/objc/add-environment-variables-and-program-arguments.html#add-environment-variables).

* If your tool is `ECLIPSE`, please refer to [Debugging the Eclipse IDE for Java Developers](https://www.eclipse.org/community/eclipse_newsletter/2017/june/article1.php) and [Eclipse Environment Variable Setup](https://examples.javacodegeeks.com/desktop-java/ide/eclipse/eclipse-environment-variable-setup-example/).

## Verify This Sample

1.  Verify in your app’s logs that similar messages were posted:

```shell
Sent message to Event Hub
Received message: Test event - graalvm
```
