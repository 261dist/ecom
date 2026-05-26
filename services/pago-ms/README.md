# pago-ms

Microservicio de pagos. Consume `orden-eventos` y publica `pago-eventos`.

## Puertos

| Recurso | DEV | PROD Docker |
|---|---:|---:|
| App | dinámico (`server.port: 0`) | 29061 -> 8080 |
| PostgreSQL | 15435 | 25435 -> 5432 |
| Kafka | 41092 | 29092 |

## DEV (Maven)

```bash
cd kafka && docker compose -f compose-dev.yml up -d
cd ../services/pago-ms
docker compose -f compose-dev.yml up -d
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

## PROD (Docker)

```bash
cd services/pago-ms
docker compose up -d --build
```

Links:
- Eureka PROD: http://localhost:28761
- Gateway PROD: http://localhost:28080
- Directo al servicio: http://localhost:29061/actuator/health
- Base de datos: `localhost:25435`

## Ver la BD desde un IDE

| Campo | Valor |
|---|---|
| Motor | PostgreSQL |
| Host | `localhost` |
| Puerto | `25435` |
| Database | `ecom_pago_db` |
| User | `ecom` |
| Password | `ecom` |

## Eventos

- Consume: `orden-eventos`
- Publica: `pago-eventos`
