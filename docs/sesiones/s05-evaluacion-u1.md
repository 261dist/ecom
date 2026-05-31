# S5 - Evaluacion Unidad 1

## Ubicacion en el curso

- Unidad: U1 - Sistema distribuido base con Spring Cloud.
- Producto de unidad: Sistema distribuido base configurable, registrado, accesible por Gateway y preparado para multiples instancias.
- Avance del producto en esta sesion: evaluacion integrada del producto U1.

## Proposito

Verificar que el estudiante puede levantar y explicar la base distribuida del sistema.

## Resultado de aprendizaje

El estudiante demuestra un sistema base funcional con Config Server, Eureka, Gateway, microservicios y bases de datos.

## Producto de sesion

Producto U1 funcionando como un todo.

## Concepto distribuido clave

La arquitectura base se valida como composicion de servicios independientes que cooperan por red.

## Implementacion en el proyecto

No se agrega tecnologia nueva. Se integra lo construido en S1-S4.

## Pasos para construir el producto de sesion

1. Preparar una lista de arranque del sistema base.
2. Levantar Config Server y validar configuraciones.
3. Levantar Eureka y validar dashboard.
4. Levantar Gateway y validar health.
5. Levantar microservicios con sus bases de datos.
6. Ejecutar una segunda instancia de al menos un microservicio.
7. Probar rutas por Gateway.
8. Recolectar evidencias: Config, Eureka, Gateway, BD y respuesta HTTP.

## Archivos involucrados

| Archivo | Proposito |
|---|---|
| `infra/*` | Infraestructura Spring Cloud |
| `services/*` | Microservicios |
| `docs/sesiones/s01..s04` | Evidencias previas |

## Comandos de ejecucion

### PowerShell

```powershell
cd infra/config; mvn spring-boot:run
cd infra/eureka; mvn spring-boot:run
cd infra/gateway; mvn spring-boot:run
```

### bash macOS/Linux

```bash
cd infra/config && mvn spring-boot:run
cd infra/eureka && mvn spring-boot:run
cd infra/gateway && mvn spring-boot:run
```

## Verificacion funcional

- Config DEV responde.
- Eureka muestra servicios.
- Gateway responde health.
- Gateway enruta a microservicios.
- Al menos un microservicio tiene dos instancias.

## Observabilidad y diagnostico

- Config Server health.
- Eureka dashboard.
- Gateway health y logs.
- Logs de microservicios.

## Verificacion de base de datos

Cada grupo debe inspeccionar al menos una BD con `psql`.

## Evidencia esperada

- Capturas o salidas de comandos.
- Explicacion del flujo Config -> Eureka -> Gateway -> Microservicio.
- Prueba de multiples instancias.

## Errores frecuentes

| Problema | Causa probable | Solucion |
|---|---|---|
| Gateway no enruta | Falta servicio en Eureka | Revisar registro |
| Config no responde | Config Server apagado | Levantar `infra/config` |

## Preguntas de defensa

1. Que componente es el punto unico de entrada?
2. Que componente resuelve configuracion externa?
3. Como se evidencia el escalado horizontal?

## Checklist de cierre

- [ ] Producto U1 levantado.
- [ ] Evidencia presentada.
- [ ] Preguntas tecnicas respondidas.
