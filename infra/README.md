# infra

Infraestructura base del sistema distribuido: Config Server, Eureka Server y API Gateway.

## Componentes

| Directorio | Puerto host PROD | Puerto container | Rol |
|---|---:|---:|---|
| `config/` | 28888 | 8888 | Configuración centralizada |
| `eureka/` | 28761 | 8761 | Service discovery |
| `gateway/` | 28080 | 8080 | Punto único de entrada HTTP + JWT |

---

## DEV (Maven local)

Levantar cada servicio en su propia terminal, en este orden:

```bash
cd config    && mvn spring-boot:run   # http://localhost:8888
cd ../eureka && mvn spring-boot:run   # http://localhost:8761
cd ../gateway && mvn spring-boot:run  # http://localhost:8080
```

**Links:**
- Config Server: http://localhost:8888/catalogo-ms/dev
- Eureka Dashboard: http://localhost:8761
- Gateway: http://localhost:8080

> Los servicios backend Maven se conectan a estos puertos (8888, 8761, 8080).
> El Docker compose de infra usa puertos distintos (28888, 28761, 28080) para no pisarlos.

---

## PROD (Docker)

```bash
# Docker compila las imágenes y levanta todo (respeta dependencias)
docker compose up -d --build
```

Gateway espera a que Eureka esté saludable; Eureka espera a Config. Cada healthcheck usa el endpoint `/actuator/health` (hasta 40s de gracia inicial).

**Links:**
- Config Server: http://localhost:28888/catalogo-ms/prod
- Eureka Dashboard: http://localhost:28761
- Gateway health: http://localhost:28080/actuator/health

> `config` no se registra en Eureka. `eureka` y `gateway` aparecen en el dashboard.

Gateway necesita `JWT_SECRET` en `infra/.env`. Debe coincidir con el `JWT_SECRET` de `services/auth-ms/.env` para validar los tokens emitidos por auth.

Detalle específico del gateway: [`gateway/README.md`](gateway/README.md).

---

Documentación completa en [`../docs/`](../docs/).
