# obs

Stack de observabilidad: Prometheus, Loki, Promtail y Grafana.

## Componentes

| Servicio | PROD | DEV |
|---|---|---:|
| Prometheus | :29090 | :19090 |
| Loki | :23100 | :13100 |
| Grafana | :23000 | :13000 |

## Inicio rápido

```bash
# PROD (red ecom-prod-net)
docker compose up -d

# DEV (red ecom-dev-net)
docker compose -f compose-dev.yml up -d
```

Documentación completa en [`../docs/`](../docs/).
