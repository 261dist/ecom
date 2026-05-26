# catalogo-ms

Microservicio de catálogo. Gestiona categorías y es consumido por `producto-ms` vía Feign.

## Puertos

| Recurso | DEV | PROD Docker |
|---|---:|---:|
| App | dinámico (`server.port: 0`) | sin puerto host (vía Gateway) |
| PostgreSQL | 15432 | 25432 -> 5432 |

## DEV (Maven)

```bash
cd services/catalogo-ms
docker compose -f compose-dev.yml up -d
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

Ver en Eureka DEV: http://localhost:18761

## PROD (Docker)

```bash
cd services/catalogo-ms
docker compose up -d --build --scale catalogo-ms=3
```

Para cambiar la cantidad de réplicas sin reconstruir:

```bash
docker compose up -d --scale catalogo-ms=2
docker compose up -d --scale catalogo-ms=3
```

Links:
- Eureka PROD: http://localhost:28761
- Gateway PROD: http://localhost:28080
- Base de datos: `localhost:25432`

## Ver la BD desde un IDE

Conéctate desde DBeaver, DataGrip, pgAdmin o IntelliJ Database con:

| Campo | Valor |
|---|---|
| Motor | PostgreSQL |
| Host | `localhost` |
| Puerto | `25432` |
| Database | `ecom_catalogo_db` |
| User | `ecom` |
| Password | `ecom` |

La BD no se escala. Las réplicas de `catalogo-ms` comparten la misma BD `ecom-postgres-catalogo` dentro de Docker.

## Endpoints

- `GET /api/v1/categorias`
- `POST /api/v1/categorias`
- `GET /api/v1/categorias/{id}`
- `PUT /api/v1/categorias/{id}`
- `DELETE /api/v1/categorias/{id}`
- `GET /api/v1/catalogo/instancia`
- `GET /actuator/health`
