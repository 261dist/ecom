# kafka

Cluster Kafka en modo KRaft (sin Zookeeper) con exporter y UI.

## Servicios

- **kafka** — broker KRaft (`:9092` interno, `:41092` externo dev)
- **kafka-exporter** — métricas para Prometheus (`:9308`)
- **kafka-ui** — consola web (`:28080`)

## Inicio rápido

```bash
# PROD (red ecom-prod-net)
docker compose up -d

# DEV (red ecom-dev-net)
docker compose -f compose-dev.yml up -d
```

Documentación completa en [`../docs/`](../docs/).
