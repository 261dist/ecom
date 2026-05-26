# orden-ms

Microservicio de órdenes. Publica eventos `orden.creada` en Kafka.

## Puertos

| Recurso | DEV | PROD Docker |
|---|---:|---:|
| App | 19051 | 29051 -> 8080 |
| PostgreSQL | 15434 | 25434 -> 5432 |
| Kafka | 41092 | 29092 |

## DEV (Maven)

```bash
cd kafka && docker compose -f compose-dev.yml up -d
cd ../services/orden-ms
docker compose -f compose-dev.yml up -d
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

## PROD (Docker)

```bash
cd services/orden-ms
docker compose up -d --build
```

Links:
- Eureka PROD: http://localhost:28761
- Gateway PROD: http://localhost:28080
- Directo al servicio: http://localhost:29051/actuator/health
- Base de datos: `localhost:25434`

## Ver la BD desde un IDE

| Campo | Valor |
|---|---|
| Motor | PostgreSQL |
| Host | `localhost` |
| Puerto | `25434` |
| Database | `ecom_orden_db` |
| User | `ecom` |
| Password | `ecom` |

## Eventos

- Publica: `orden-eventos`
- Consume: `pago-eventos`
