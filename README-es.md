# Spring Boot RabbitMQ Producer with Direct Exchange

Este proyecto es un ejemplo de cómo utilizar Spring Boot con RabbitMQ para enviar mensajes utilizando un `DirectExchange`. La configuración define dos colas (`queue.A` y `queue.B`), cada una con su propia clave de enrutamiento.

## Estructura del Proyecto

### Paquetes principales:

1. **top.anyel.rabbit.controllers**: Contiene el controlador REST que expone un endpoint para enviar mensajes a RabbitMQ.

2. **top.anyel.rabbit.config**: Configuración de RabbitMQ, incluyendo colas, exchange, bindings, y converter.

3. **top.anyel.rabbit.models**: Define el modelo `Message`, que es el objeto que se envía a RabbitMQ.

## Configuración de RabbitMQ

La configuración se encuentra en la clase `RabbitMQConfigBinding` en el paquete `top.anyel.rabbit.config`. Aquí se define lo siguiente:

- **Colas**:
    - `queue.A`
    - `queue.B`

- **Exchange**:
    - `exchange.direct`

- **Bindings**:
    - `queue.A` está enlazada a `exchange.direct` con la clave de enrutamiento `routing.A`.
    - `queue.B` está enlazada a `exchange.direct` con la clave de enrutamiento `routing.B`.

- **MessageConverter**:
    - Se utiliza `Jackson2JsonMessageConverter` para convertir mensajes a formato JSON.

## Endpoints

El proyecto expone un único endpoint para enviar mensajes:

- **POST /post**
    - Envía un mensaje a RabbitMQ utilizando la clave de enrutamiento `routing.A`.
    - El mensaje debe estar en formato JSON y debe tener la estructura definida en el modelo `Message`.

### Ejemplo de cuerpo del mensaje:

```json
{
  "id": 1,
  "name": "Test Message"
}
```

## Configuración de la Aplicación

Asegúrate de ajustar la configuración de conexión a RabbitMQ en el archivo `application.properties`:

```properties
spring.application.name=SpringBoot-RabbitMQ-Producer-Direct

# Rabbit connection
spring.rabbitmq.host=192.168.1.111
spring.rabbitmq.port=5672
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
```

## Cómo ejecutar el proyecto

1. Asegúrate de que RabbitMQ esté corriendo y sea accesible en la dirección especificada en `application.properties`.

2. Clona este repositorio y navega al directorio del proyecto.

3. Ejecuta el proyecto utilizando Maven o tu IDE preferido.

4. Usa herramientas como `curl` o Postman para enviar una petición POST al endpoint `/post`.

## Contribuciones

Las contribuciones son bienvenidas. Puedes abrir issues o enviar pull requests para mejorar el proyecto.
