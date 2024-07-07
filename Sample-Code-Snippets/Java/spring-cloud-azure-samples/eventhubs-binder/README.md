---
page_type: sample
languages:
- java
products:
- azure-event-hubs
name: Sending and Receiving Message by Azure Event Hubs and Spring Cloud Stream Binder Eventhubs in Spring Boot Application
description: This sample demonstrates how to send and receive message by Azure Event Hubs and Spring Cloud Stream Binder EventHubs in Spring Boot application.
---

# Sending and Receiving Message by Azure Event Hubs and Spring Cloud Stream Binder Eventhubs in Spring Boot Application

>The project is copied and adapted from [    azure-spring-boot-samples/eventhubs/spring-cloud-azure-starter-eventhubs/eventhubs-client](https://github.com/Azure-Samples/azure-spring-boot-samples/tree/8a6ccc248fd6c61f3bec4470eb453238fe77bfd5/eventhubs/spring-cloud-azure-starter-eventhubs/eventhubs-client)

This code sample demonstrates how to use the `Spring Cloud Stream Binder` for `Azure Event Hubs`.The
sample app has two operating modes.
One way is to expose a Restful API to receive string message, another way is to automatically provide string messages.
These messages are published to one `Event Hub` instance and then consumed by one consumer
endpoint from the same application.

## What You Will Build
You will build an application using `Spring Cloud Stream Binder` to send and receive messages for `Azure Event Hubs`.

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
New message received: 'Hello world, 17' ...
Message 'Hello world, 17' successfully checkpointed
...
New message received: 'Hello world, 18' ...
Message 'Hello world, 18' successfully checkpointed
...
New message received: 'Hello world, 27' ...
Message 'Hello world, 27' successfully checkpointed

```

## Enhancement

### [Enable sync message](https://aka.ms/spring/docs/4.0.0#producer-properties)

To enable message sending in a synchronized way with Spring Cloud Stream 3.x, spring-cloud-azure-stream-binder-eventhubs supports the sync producer mode to get responses for sent messages. 
Below classes are sample to use the sync mode:
```
ImperativeEventProducerController.java
ManualProducerAndConsumerConfiguration.java   
ReactiveEventProducerController.java
```
Try the sync mode with the "manual" profile after setting `spring.cloud.stream.eventhubs.bindings.<binding-name>.producer.sync=true`. In this sample, the binding-name should be `supply-out-0`. Users can run the following commands:
```
mvn clean spring-boot:run -Dspring-boot.run.profiles=manual

$ ### Send messages through imperative.  
curl -X POST http://localhost:8080/messages/imperative?message=hello

$ ### Send messages through reactive.
curl -X POST http://localhost:8080/messages/reactive?message=hello
```
or when the app runs on App Service or VM
```
$ ### Send messages through imperative.
curl -d -X POST https://[your-app-URL]/messages/imperative?message=hello

$ ### Send messages through reactive.
curl -d -X POST https://[your-app-URL]/messages/reactive?message=hello
```
Verify in your app’s logs that a similar message was posted:
```
New message received: 'hello', partition key: 2002572479, sequence number: 4, offset: 768, enqueued time: 2021-06-03T01:47:36.859Z
Message 'hello' successfully checkpointed
```

### [Using Batch Consuming](https://aka.ms/spring/docs/4.0.0#batch-consumer-support)

To work with the batch-consumer mode, the property of spring.cloud.stream.bindings.<binding-name>.consumer.batch-mode should be set as true. When enabled, an org.springframework.messaging.Message of which the payload is a list of batched events will be received and passed to the consumer function.

In this sample, users can try the batch-consuming mode by enabling the "batch" profile and fill the "application-batch.yml". For more details about how to work in batch-consuming mode, please refer to the [reference doc](https://aka.ms/spring/docs/4.0.0#batch-consumer-support-2).

### Set Event Hubs message headers

Users can get all the supported EventHubs message headers [here](https://aka.ms/spring/docs/4.0.0#scs-eh-headers) to configure.

### Resource Provision

Event Hubs binder supports provisioning of event hub and consumer group, users could use [properties](https://aka.ms/spring/docs/4.0.0#resource-provision) to enable provisioning.

### Partitioning Support

A PartitionSupplier with user-provided partition information will be created to configure the partition information about the message to be sent. The binder supports Event Hubs partitioning by allowing setting partition key and id. Please refer to the [reference doc](https://aka.ms/spring/docs/4.0.0#partitioning-support-2) for more details.

### Error Channel

Event Hubs binder supports consumer error channel, producer error channel and global default error channel, click [here](https://aka.ms/spring/docs/4.0.0#error-channels) to see more information.
