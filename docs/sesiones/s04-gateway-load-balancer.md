# S4 - Gateway y balanceo de carga

## Ubicacion en el curso

- Unidad: U1 - Sistema distribuido base con Spring Cloud.
- Producto de unidad: Sistema distribuido base configurable, registrado, accesible por Gateway y preparado para multiples instancias.
- Avance del producto en esta sesion: Gateway operativo con rutas y balanceo entre instancias.

## Proposito

Exponer un punto unico de entrada al sistema y distribuir peticiones hacia servicios registrados en Eureka.

## Resultado de aprendizaje

El estudiante consume servicios por Gateway, verifica rutas y demuestra balanceo entre multiples instancias.

## Producto de sesion

- Gateway levantado.
- Rutas hacia microservicios.
- Consumo por `localhost:18080`.
- Balanceo entre instancias.

## Concepto distribuido clave

El Gateway centraliza acceso, politicas transversales y enrutamiento. El load balancing distribuye peticiones entre instancias disponibles.

## Implementacion en el proyecto

Gateway vive en `infra/gateway` y lee rutas desde Config Server.

## Pasos para construir el producto de sesion

1. Crear el proyecto `infra/gateway` con Spring Cloud Gateway.
2. Configurar el puerto DEV del Gateway.
3. Conectar Gateway a Config Server y Eureka.
4. Definir rutas por prefijo, por ejemplo `/api/v1/categorias/**`.
5. Usar `lb://nombre-servicio` para enrutar por nombre logico de Eureka.
6. Levantar dos instancias de un microservicio destino.
7. Enviar varias peticiones por Gateway y observar distribucion en logs.
8. Documentar que los clientes consumen Gateway, no microservicios directos.

## Archivos involucrados

| Archivo | Proposito |
|---|---|
| `infra/gateway/src/main/resources/application.yml` | Puerto local del Gateway |
| `infra/config/config-repo/gateway-dev.yml` | Rutas DEV |
| `infra/gateway/src/main/java/.../SecurityConfig.java` | Permisos y seguridad |

## Comandos de ejecucion

### PowerShell

```powershell
cd infra/gateway
mvn spring-boot:run

Invoke-RestMethod -Method Get -Uri "http://localhost:18080/actuator/health"
Invoke-RestMethod -Method Get -Uri "http://localhost:18080/api/v1/categorias"
```

### bash macOS/Linux

```bash
cd infra/gateway
mvn spring-boot:run

curl http://localhost:18080/actuator/health
curl http://localhost:18080/api/v1/categorias
```

## Verificacion funcional

Consumir microservicios solo por Gateway DEV:

```text
http://localhost:18080/api/v1/categorias
```

## Observabilidad y diagnostico

- Gateway health: `http://localhost:18080/actuator/health`.
- Logs de Gateway al enrutar.
- Eureka para verificar instancias disponibles.
- Logs de microservicios para observar distribucion.

## Verificacion de base de datos

```powershell
docker exec -it ecom-postgres-catalogo-dev psql -U ecom -d ecom_catalogo_db -c "SELECT * FROM categorias;"
```

## Evidencia esperada

- Gateway responde health.
- Endpoint por Gateway responde.
- Se observa uso de multiples instancias.

## Errores frecuentes

| Problema | Causa probable | Solucion |
|---|---|---|
| 503 | Servicio no registrado | Revisar Eureka |
| 401 | Ruta protegida | Usar token o probar ruta publica |

## Preguntas de defensa

1. Por que el frontend no consume microservicios directos?
2. Como sabe Gateway a que instancia enviar una peticion?
3. Que diferencia hay entre Gateway y Eureka?

## Checklist de cierre

- [ ] Gateway activo.
- [ ] Ruta publica funcionando.
- [ ] Rutas revisadas en Config Server.
- [ ] Balanceo demostrado.
