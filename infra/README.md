# infra

Infraestructura base del sistema distribuido: Config Server, Eureka Server y API Gateway.

## Componentes

| Directorio | Puerto PROD | Rol |
|---|---|---:|
| `config/` | 8888 | Configuración centralizada |
| `eureka/` | 8761 | Service discovery |
| `gateway/` | 8090 | Punto único de entrada HTTP + JWT |

## Inicio rápido

```bash
# Todos los servicios de infra
docker compose up -d

# O individualmente con Maven (dev)
cd config    && mvn spring-boot:run   # :8888
cd ../eureka && mvn spring-boot:run   # :8761
cd ../gateway && mvn spring-boot:run  # :8080 local
```

Documentación completa en [`../docs/`](../docs/).
