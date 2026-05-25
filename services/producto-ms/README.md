# producto-ms

Microservicio de productos. Consume `catalogo-ms` vía OpenFeign con Circuit Breaker (Resilience4j).

## Stack

Java 17, Spring Boot 3.5, PostgreSQL, Flyway, Eureka Client, Config Client, OpenFeign, Resilience4j, Spring Security (JWT resource server), SpringDoc OpenAPI

## Puertos

| Recurso | DEV | PROD |
|---|---|---:|
| App | 0 (dinámico) | 8080 (int) / 9092 (host) |
| PostgreSQL | 5407 | 5408 |

---

## DEV (Maven local)

```bash
# 1. Infraestructura
cd infra && docker compose up -d
# http://localhost:8099 — Config Server
# http://localhost:8761 — Eureka Dashboard

# 2. PostgreSQL dev (si no usas Docker para BD)
# docker compose -f compose-dev.yml up -d

# 3. Desde services/producto-ms/
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

**Link útil:** http://localhost:8761 (verificar que `PRODUCTO-MS` aparezca en Eureka)

---

## PROD (Docker)

```bash
# 1. Infraestructura
cd infra && docker compose up -d

# 2. producto-ms + su BD
cd services/producto-ms && docker compose up -d
```

**Links:**
- API Gateway: http://localhost:8090
- Eureka Dashboard: http://localhost:8761

---

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
