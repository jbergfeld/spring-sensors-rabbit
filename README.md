# Demo Spring Sensors application

## Prerequisites

This application acts as a consumer of sensor data which the application stores in an in-memory database and displays on a dashboard.

[Spring Cloud Stream](https://spring.io/projects/spring-cloud-stream), a framework built on top of Spring Boot and Spring Integration, is used as a flexible messaging abstraction. 
Spring Cloud Stream supports a variety of binder implementations. In this case, we are using the one for RabbitMQ.

## Deploying the publisher

The sensor data is generated and sent by [this](https://github.com/jbergfeld/spring-sensors-publisher) application via asynchronous messaging.

## Deploying the application

To build and store the client container: (ensure JAVA_HOME points to an installed JDK and a Docker daemon is running)

```
./mvnw spring-boot:build-image -Dspring-boot.build-image.imageName=docker.io/library/spring-sensors-client:latest
```

```
docker tag spring-sensors-publisher:latest REGISTRY/PROJECT/spring-sensors-client:latest
```

```
docker push REGISTRY/PROJECT/spring-sensors-client:latest
```

Where REGISTRY is your container registry and PROJECT exists with the registry.

```
kubectl apply -f kubernetes-deployment.yaml
kubectl apply -f kubernetes-service.yaml
```

Note: replace the REGISTRY and PROJECT placeholders in the deployment manifest with your respective values.

