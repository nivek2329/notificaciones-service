# notificaciones-service

Parte de **Arepa Express** (DOSW · Semana 14): API Gateway en Azure API Management y eventos con RabbitMQ. Spring Boot 4.1.2 · Java 21 · Maven.

Consumidor del evento de pedido creado. Escucha su propia cola durable `notificaciones.pedidos`, unida al exchange `arepas.eventos` con la routing key `pedido.creado`, y registra el aviso al cliente. Como tiene su propia cola, recibe el mismo pedido que cocina-service (uno a muchos).

## Variables de entorno

| Variable | Uso | Valor por defecto (local) |
|---|---|---|
| `RABBIT_HOST` | host de RabbitMQ | `localhost` |
| `RABBIT_USER` | usuario | `arepas` |
| `RABBIT_PASS` | clave | `arepas123` |

Para probar en local: `docker run -d -p 5672:5672 -p 15672:15672 -e RABBITMQ_DEFAULT_USER=arepas -e RABBITMQ_DEFAULT_PASS=arepas123 rabbitmq:3-management`

## Cómo ejecutarlo

```bash
./mvnw spring-boot:run          # local (puerto 8080)
./mvnw -q package -DskipTests   # genera target/*.jar
docker build -t notificaciones-service .           # imagen con el Dockerfile del repo
```
