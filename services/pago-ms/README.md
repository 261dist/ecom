# pago-ms

Microservicio de pagos. Consume eventos de `orden-eventos` (Kafka), procesa pago simulado, publica resultado en `pago-eventos`.

## Stack

Java 17, Spring Boot 3.5, PostgreSQL, Kafka, Eureka Client, Config Client

## Puertos

| Recurso | DEV | PROD |
|---|---|---:|
| App | 19061 (int) / dinámico | 29061 |
| PostgreSQL | 19060 | 29060 |
| Kafka | localhost:41092 | kafka:9092 |

## Eventos

- **Consume:** `orden-eventos` (orden.creada)
- **Publica:** `pago-eventos` (resultado del pago)

---

## DEV (Maven local)

```bash
# 1. Infraestructura
cd infra && docker compose up -d
# http://localhost:8099 — Config Server
# http://localhost:8761 — Eureka Dashboard

# 2. Kafka dev
cd kafka && docker compose -f compose-dev.yml up -d

# 3. Desde services/pago-ms/
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

**Link útil:** http://localhost:8761 (verificar que `PAGO-MS` aparezca en Eureka)

---

## PROD (Docker)

```bash
# 1. Infraestructura
cd infra && docker compose up -d

# 2. Kafka prod
cd kafka && docker compose up -d

# 3. pago-ms + su BD
cd services/pago-ms && docker compose up -d
```

**Links:**
- API Gateway: http://localhost:8090
- Eureka Dashboard: http://localhost:8761

---

## Variables de entorno

| Variable | Descripción |
|---|---|
| `DB_HOST` | Host PostgreSQL |
| `DB_PORT` | Puerto PostgreSQL |
| `DB_NAME` | Base de datos |
| `DB_USER` | Usuario BD |
| `DB_PASS` | Contraseña BD |
| `CONFIG_SERVER_URL` | URL del Config Server |
| `KAFKA_BOOTSTRAP_SERVERS` | Brokers Kafka |

## Documentación

Ver [`docs/sesiones/s07-kafka-ingesta.md`](../docs/sesiones/s07-kafka-ingesta.md) y [`docs/sesiones/s08-kafka-observabilidad.md`](../docs/sesiones/s08-kafka-observabilidad.md).
