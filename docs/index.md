# ecom — Plataforma de Microservicios 2026

Proyecto educativo de arquitectura distribuida con Spring Boot, Spring Cloud, PostgreSQL, Kafka y observabilidad.

## Estructura del proyecto

```
ecom/                      ← raíz del monorepositorio
├── infra/                 ← infraestructura base (config, eureka, gateway)
├── services/              ← microservicios backend (-ms)
├── clients/               ← frontends (-ng)
├── kafka/                 ← plataforma de eventos (EDA)
├── obs/                   ← observabilidad (Prometheus, Loki, Grafana)
├── docs/                  ← libro digital (MkDocs Material)
└── extras/                ← aprendizaje y experimentos
```

## Componentes

| Componente | Dentro de | Rol | Puerto host PROD | Puerto container |
|---|---|---|---:|---:|
| **Config Server** | `infra/config/` | Configuración centralizada | 8099 | 8099 |
| **Eureka Server** | `infra/eureka/` | Service discovery | 8761 | 8761 |
| **API Gateway** | `infra/gateway/` | Punto único de entrada + JWT | 8090 | 8080 |
| **auth-ms** | `services/auth-ms/` | Autenticación y emisión JWT | 8042 | 8080 |
| **catalogo-ms** | `services/catalogo-ms/` | Gestión de categorías | 8082 | 8080 |
| **producto-ms** | `services/producto-ms/` | Gestión de productos + Feign + CB | 9092 | 8080 |
| **orden-ms** | `services/orden-ms/` | Órdenes + Kafka producer | 29051 | 8080 |
| **pago-ms** | `services/pago-ms/` | Pagos + Kafka consumer | 29061 | 8080 |
| **ecom-ng** | `clients/ecom-ng/` | SPA Angular (frontend) | — | — |

> Los servicios backend usan `server.port: 0` (aleatorio) en desarrollo local y `server.port: 8080` en Docker.

## Stack

- Java 17, Spring Boot 3.5, Spring Cloud 2025
- PostgreSQL 16, Flyway
- Kafka (KRaft mode, sin Zookeeper)
- Prometheus, Loki, Grafana
- Docker Compose
- Angular 19 (cliente web)

## Inicio rápido

### DEV (Maven local)

```bash
# 1. Crear redes Docker (una sola vez, si no existen)
docker network create ecom-prod-net
docker network create ecom-dev-net

# 2. Infraestructura (Config, Eureka)
cd infra && docker compose up -d
#   http://localhost:8099 — Config Server
#   http://localhost:8761  — Eureka Dashboard

# 3. Servicios (cada uno en su terminal)
cd services/auth-ms      && mvn spring-boot:run -Dspring-boot.run.profiles=dev
cd services/catalogo-ms  && mvn spring-boot:run -Dspring-boot.run.profiles=dev
cd services/producto-ms  && mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

### PROD (Docker)

```bash
# 1. Redes (una sola vez)
docker network create ecom-prod-net

# 2. Infraestructura
cd infra && docker compose up -d
#   http://localhost:8099 — Config Server
#   http://localhost:8761  — Eureka Dashboard
#   http://localhost:8090  — API Gateway

# 3. Servicios
cd services/auth-ms      && docker compose up -d
cd services/catalogo-ms  && docker compose up -d
cd services/producto-ms  && docker compose up -d
cd services/orden-ms     && docker compose up -d
cd services/pago-ms      && docker compose up -d
```

## Puertos de desarrollo (PostgreSQL)

| Servicio | DB | Puerto host dev | Puerto interno |
|---|---|---|---:|
| auth-ms | `ecom_auth_db` | 5401 | 5432 |
| catalogo-ms | `ecom_catalogo_db` | 5404 | 5432 |
| producto-ms | `ecom_producto_db` | 5407 | 5432 |
| orden-ms | `ecom_orden_db` | 5405 | 5432 |
| pago-ms | `ecom_pago_db` | 5406 | 5432 |

Credenciales: `ecom` / `ecom`
