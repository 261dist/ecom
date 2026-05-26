# producto-ms

Microservicio de productos. Consume `catalogo-ms` vía OpenFeign con Circuit Breaker.

## Puertos

| Recurso | DEV | PROD Docker |
|---|---:|---:|
| App | dinámico (`server.port: 0`) | 9092 -> 8080 |
| PostgreSQL | 15433 | 25433 -> 5432 |

## DEV (Maven)

```bash
cd services/producto-ms
docker compose -f compose-dev.yml up -d
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

Ver en Eureka DEV: http://localhost:18761

## PROD (Docker)

```bash
cd services/producto-ms
docker compose up -d --build
```

Links:
- Eureka PROD: http://localhost:28761
- Gateway PROD: http://localhost:28080
- Directo al servicio: http://localhost:9092/actuator/health
- Base de datos: `localhost:25433`

## Ver la BD desde un IDE

| Campo | Valor |
|---|---|
| Motor | PostgreSQL |
| Host | `localhost` |
| Puerto | `25433` |
| Database | `ecom_producto_db` |
| User | `ecom` |
| Password | `ecom` |

## Endpoints

- `GET /api/v1/productos`
- `POST /api/v1/productos`
- `GET /api/v1/productos/{id}`
- `PUT /api/v1/productos/{id}`
- `DELETE /api/v1/productos/{id}`
- `GET /api/v1/producto/instancia`
- `GET /actuator/health`
