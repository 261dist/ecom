# auth-ms

Microservicio de autenticación. Emite JWT con roles para el control de acceso distribuido.

## Stack

Java 17, Spring Boot 3.5, Spring Security, JWT (jjwt), PostgreSQL, Flyway, Eureka Client, Config Client

## Puertos

| Recurso | DEV | PROD |
|---|---|---:|
| App | 0 (dinámico) | 8080 (int) / 8042 (host) |
| PostgreSQL | 5401 | 5402 |

## Ejecutar local

```bash
# 1. Levantar infraestructura
cd infra && docker compose up -d

# 2. Desde services/auth-ms/
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

## Endpoints

- `POST /auth/login` — login, devuelve JWT
- `POST /auth/register` — registrar usuario
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
| `JWT_SECRET` | Clave secreta JWT (solo prod) |

## Seguridad

- `gateway` valida JWT en el borde
- `producto` valida JWT como resource server
- `catalogo` se protege solo desde gateway

## Documentación

Ver [`docs/sesiones/s06-seguridad.md`](../docs/sesiones/s06-seguridad.md).
