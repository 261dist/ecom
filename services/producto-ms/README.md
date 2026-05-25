# producto-ms

Microservicio de productos. Consume `catalogo-ms` vía OpenFeign con Circuit Breaker (Resilience4j).

## Stack

Java 17, Spring Boot 3.5, PostgreSQL, Flyway, Eureka Client, Config Client, OpenFeign, Resilience4j, Spring Security (JWT resource server), SpringDoc OpenAPI

## Puertos

| Recurso | DEV | PROD |
|---|---|---:|
| App | 0 (dinámico) | 8080 (int) / 9092 (host) |
| PostgreSQL | 5407 | 5408 |

## Ejecutar local

```bash
# 1. Levantar infraestructura
cd infra && docker compose up -d

# 2. Desde services/producto-ms/
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

## Endpoints

- `GET /api/v1/productos` — listar productos
- `POST /api/v1/productos` — crear producto
- `GET /api/v1/productos/{id}` — obtener por ID (incluye categoría vía Feign)
- `PUT /api/v1/productos/{id}` — actualizar
- `DELETE /api/v1/productos/{id}` — eliminar
- `GET /api/v1/producto/instancia` — info de instancia
- `GET /actuator/health`

## Circuit Breaker

El método `findDetalleById` consulta `catalogo-ms` vía Feign con un Circuit Breaker nombre `catalogo`. Si falla, usa `fallbackCategoria`.

## Variables de entorno

| Variable | Descripción |
|---|---|
| `DB_HOST` | Host PostgreSQL |
| `DB_PORT` | Puerto PostgreSQL |
| `DB_NAME` | Base de datos |
| `DB_USER` | Usuario BD |
| `DB_PASS` | Contraseña BD |
| `CONFIG_SERVER_URL` | URL del Config Server |
| `JWT_SECRET` | Clave secreta JWT (solo prod) |

## Documentación

Ver [`docs/sesiones/s06-seguridad.md`](../docs/sesiones/s06-seguridad.md).
