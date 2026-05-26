# kafka

Cluster Kafka en modo KRaft (sin Zookeeper) con exporter y UI.

## Servicios

| Servicio | Puerto host DEV | Puerto host PROD |
|---|---:|---:|
| Kafka broker | 41092 | 28092 |
| Kafka UI | 41085 | 28085 |
| Kafka Exporter | 41308 | 29308 |

## Inicio rápido

```bash
# DEV (red ecom-dev-net)
docker compose -f compose-dev.yml up -d
#   http://localhost:41085 — Kafka UI

# PROD (red ecom-prod-net)
docker compose up -d
#   http://localhost:28085 — Kafka UI
```

Documentación en [`../docs/`](../docs/).
