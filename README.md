# ecom — Plataforma de Microservicios 2026

Proyecto educativo de microservicios con Spring Boot, Spring Cloud, PostgreSQL, Kafka y observabilidad.

## Stack

Java 17, Spring Boot 3.5, Spring Cloud, PostgreSQL 16, Kafka, Prometheus, Loki, Grafana, Angular 21

---

## Inicio rápido (DEV) — Maven local

```bash
# 1. Redes Docker (una sola vez)
docker network create ecom-prod-net
docker network create ecom-dev-net

# 2. Infraestructura (Maven, cada uno en su terminal)
cd infra/config    && mvn spring-boot:run   # http://localhost:8888
cd infra/eureka    && mvn spring-boot:run   # http://localhost:8761
cd infra/gateway   && mvn spring-boot:run   # http://localhost:8080

# 3. PostgreSQL para cada servicio que vayas a levantar
cd services/auth-ms     && docker compose -f compose-dev.yml up -d   # :15431
cd services/catalogo-ms && docker compose -f compose-dev.yml up -d   # :15432
cd services/producto-ms && docker compose -f compose-dev.yml up -d   # :15433

# 4. Microservicios (cada uno en su terminal)
cd services/auth-ms      && mvn spring-boot:run -Dspring-boot.run.profiles=dev
cd services/catalogo-ms  && mvn spring-boot:run -Dspring-boot.run.profiles=dev
cd services/producto-ms  && mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

## Inicio rápido (PROD) — Docker

```bash
# 1. Red
docker network create ecom-prod-net

# 2. Levantar infraestructura (Docker compila las imágenes)
cd infra && docker compose up -d --build
#   http://localhost:28888 — Config Server
#   http://localhost:28761  — Eureka Dashboard
#   http://localhost:28080  — API Gateway

# 3. Servicios (Docker compila cada imagen)
cd ../services/auth-ms      && docker compose up -d --build
cd ../catalogo-ms           && docker compose up -d --build
cd ../producto-ms           && docker compose up -d --build
cd ../orden-ms              && docker compose up -d --build
cd ../pago-ms               && docker compose up -d --build
```

Para modo mixto (Maven + Docker): arranca infra en Docker y pasa estas variables a tus servicios Maven:
```bash
CONFIG_SERVER_URL=http://localhost:28888
eureka.client.service-url.defaultZone=http://localhost:28761/eureka
```

## Puertos

| Componente | Puerto host DEV (Maven) | Puerto host PROD (Docker) |
|---|---:|---:|
| Config Server | 8888 | 28888 |
| Eureka | 8761 | 28761 |
| Gateway | 8080 | 28080 |
| auth-ms | dinámico | 8042 |
| catalogo-ms | dinámico | 8082 |
| producto-ms | dinámico | 9092 |
| orden-ms | 19051 | 29051 |
| pago-ms | 19061 | 29061 |

## Estructura

```
ecom/
├── infra/         ← Config, Eureka, Gateway
├── services/      ← auth-ms, catalogo-ms, producto-ms, orden-ms, pago-ms
├── clients/       ← ecom-ng (Angular)
├── kafka/         ← broker + UI
├── obs/           ← Prometheus, Loki, Grafana
├── docs/          ← libro digital (MkDocs)
└── extras/        ← experimentos
```

## Documentación

Libro digital: [`docs/`](docs/) (MkDocs, sirve en :8002 con `docs/compose.yml`)
