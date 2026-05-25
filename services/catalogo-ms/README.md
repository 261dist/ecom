# catalogo-ms

Microservicio de catálogo. Gestiona categorías. Consumido por `producto-ms` vía Feign.

## Stack

Java 17, Spring Boot 3.5, PostgreSQL, Flyway, Eureka Client, Config Client, SpringDoc OpenAPI

## Puertos

| Recurso | DEV | PROD |
|---|---|---:|
| App | 0 (dinámico) | 8080 (int) / 8082 (host) |
| PostgreSQL | 5404 | 5405 |

## Ejecutar local

```bash
# 1. Levantar infraestructura
cd infra && docker compose up -d

# 2. Desde services/catalogo-ms/
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

## Endpoints

- `GET /api/v1/categorias` — listar categorías
- `POST /api/v1/categorias` — crear categoría
- `GET /api/v1/categorias/{id}` — obtener por ID
- `PUT /api/v1/categorias/{id}` — actualizar
- `DELETE /api/v1/categorias/{id}` — eliminar
- `GET /api/v1/catalogo/instancia` — info de instancia
- `GET /actuator/health`

## Variables de entorno

| Variable | Descripción |
|---|---|
| `DB_HOST` | Host PostgreSQL |
| `DB_PORT` | Puerto PostgreSQL |
| `DB_NAME` | Base de datos |
| `DB_USER` | Usuario BD |
| `DB_PASS` | Contraseña BD |
| `CONFIG_SERVER_URL` | URL del Config Server |

## Documentación

Ver [`docs/sesiones/s00-infraestructura.md`](../docs/sesiones/s00-infraestructura.md).
