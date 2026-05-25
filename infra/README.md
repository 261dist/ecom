# infra

Infraestructura base del sistema distribuido: Config Server, Eureka Server y API Gateway.

## Componentes

| Directorio | Puerto PROD | Rol |
|---|---|---:|
| `config/` | 8099 | Configuración centralizada |
| `eureka/` | 8761 | Service discovery |
| `gateway/` | 8090 | Punto único de entrada HTTP + JWT |

---

## DEV (Maven local)

Levantar cada servicio en su propia terminal, en este orden:

```bash
cd config    && mvn spring-boot:run   # http://localhost:8099
cd ../eureka && mvn spring-boot:run   # http://localhost:8761
cd ../gateway && mvn spring-boot:run  # http://localhost:8080
```

**Links:**
- Config Server: http://localhost:8099/catalogo-ms/dev
- Eureka Dashboard: http://localhost:8761
- Gateway: http://localhost:8080

---

## PROD (Docker)

```bash
docker compose up -d
```

**Links:**
- Eureka Dashboard: http://localhost:8761
- Gateway: http://localhost:8090

---

Documentación completa en [`../docs/`](../docs/).
