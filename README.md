# Spring Boot RabbitMQ Producer with Direct Exchange

This project is an example of how to use Spring Boot with RabbitMQ to send messages using a `DirectExchange`. The configuration defines two queues (`queue.A` and `queue.B`), each with its own routing key.

## Project Structure

### Main Packages:

1. **top.anyel.rabbit.controllers**: Contains the REST controller that exposes an endpoint to send messages to RabbitMQ.

2. **top.anyel.rabbit.config**: RabbitMQ configuration, including queues, exchange, bindings, and converter.

3. **top.anyel.rabbit.models**: Defines the `Message` model, which is the object sent to RabbitMQ.

## RabbitMQ Configuration

The configuration is located in the `RabbitMQConfigBinding` class in the `top.anyel.rabbit.config` package. It defines the following:

- **Queues**:
    - `queue.A`
    - `queue.B`

- **Exchange**:
    - `exchange.direct`

- **Bindings**:
    - `queue.A` is bound to `exchange.direct` with the routing key `routing.A`.
    - `queue.B` is bound to `exchange.direct` with the routing key `routing.B`.

- **MessageConverter**:
    - `Jackson2JsonMessageConverter` is used to convert messages to JSON format.

## Endpoints

The project exposes a single endpoint to send messages:

- **POST /post**
    - Sends a message to RabbitMQ using the routing key `routing.A`.
    - The message must be in JSON format and follow the structure defined in the `Message` model.

### Example of the message body:

```json
{
  "id": 1,
  "name": "Test Message"
}
```

## Application Configuration

Make sure to adjust the RabbitMQ connection settings in the `application.properties` file:

```properties
spring.application.name=SpringBoot-RabbitMQ-Producer-Direct

# Rabbit connection
spring.rabbitmq.host=192.168.1.111
spring.rabbitmq.port=5672
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
```

## How to Run the Project

1. Ensure RabbitMQ is running and accessible at the address specified in `application.properties`.

2. Clone this repository and navigate to the project directory.

3. Run the project using Maven or your preferred IDE.

4. Use tools like `curl` or Postman to send a POST request to the `/post` endpoint.

## Contributions

Contributions are welcome. You can open issues or submit pull requests to improve the project.