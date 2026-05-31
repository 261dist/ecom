# S10 - Consolidacion de observabilidad del sistema distribuido

## Ubicacion en el curso

- Unidad: U2 - Sistema distribuido robusto e integrado.
- Producto de unidad: Sistema distribuido seguro, resiliente, observable, orientado a eventos e integrado con frontend.
- Avance del producto en esta sesion: vista operativa del sistema completo.

## Proposito

Consolidar health checks, logs, metricas y paneles para diagnosticar fallos en el sistema distribuido.

## Resultado de aprendizaje

El estudiante identifica fallos usando evidencias observables y no solo prueba manual.

## Producto de sesion

Observabilidad integrada para infraestructura, microservicios, Kafka y Gateway.

## Concepto distribuido clave

En sistemas distribuidos, el fallo puede ocurrir en red, configuracion, servicio, base de datos, evento o cliente. La observabilidad reduce incertidumbre.

## Implementacion en el proyecto

Se usa Actuator, logs, Prometheus, Loki, Grafana y Kafka Exporter segun el alcance del entorno.

## Pasos para construir el producto de sesion

1. Exponer endpoints Actuator necesarios en cada servicio.
2. Estandarizar logs por microservicio.
3. Levantar el stack de observabilidad.
4. Configurar Prometheus para recolectar metricas.
5. Configurar Loki/Promtail si se trabaja con logs centralizados.
6. Agregar Kafka Exporter para observar Kafka.
7. Crear o revisar dashboards basicos.
8. Simular fallos y documentar como se diagnostican.

## Archivos involucrados

| Archivo | Proposito |
|---|---|
| `obs/compose-dev.yml` | Stack observabilidad DEV |
| `obs/prometheus/prometheus-dev.yml` | Scrape de metricas |
| `services/*/src/main/resources/logback-spring.xml` | Logs |
| `infra/config/config-repo/*-dev.yml` | Exposure de endpoints |

## Comandos de ejecucion

### PowerShell

```powershell
cd obs
docker compose -f compose-dev.yml up -d
```

### bash macOS/Linux

```bash
cd obs
docker compose -f compose-dev.yml up -d
```

## Verificacion funcional

- Gateway health activo.
- Kafka exporter activo.
- Grafana disponible.
- Prometheus scrapeando targets.

## Observabilidad y diagnostico

- Prometheus.
- Grafana.
- Loki.
- Logs por servicio.
- Health checks.
- Kafka UI.

## Verificacion de base de datos

No es el foco de la sesion, pero se deben correlacionar registros con flujos probados.

## Evidencia esperada

- Captura de targets Prometheus.
- Captura de Grafana o logs.
- Explicacion de un fallo diagnosticado.

## Errores frecuentes

| Problema | Causa probable | Solucion |
|---|---|---|
| Target caido | Servicio apagado o puerto incorrecto | Revisar compose y health |
| Sin logs | Volumen o config logback | Revisar `logs/` |

## Preguntas de defensa

1. Diferencia entre logging, metrica y tracing?
2. Que revisas primero ante un 503?
3. Como diagnosticas un evento Kafka no consumido?

## Checklist de cierre

- [ ] Stack obs activo.
- [ ] Health revisado.
- [ ] Logs revisados.
- [ ] Metrica o dashboard presentado.
