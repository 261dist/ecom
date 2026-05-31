# Guia del curso

## Enfoque

El curso se desarrolla como construccion incremental de un producto. Cada sesion entrega una parte verificable del sistema distribuido.

La evaluacion se concentra en cuatro capacidades:

- Implementar.
- Ejecutar.
- Diagnosticar.
- Defender tecnicamente.

## Productos por unidad

| Unidad | Producto |
|---|---|
| U1 | Sistema distribuido base configurable, registrado, accesible por Gateway y preparado para multiples instancias |
| U2 | Sistema distribuido seguro, resiliente, observable, orientado a eventos e integrado con frontend |
| U3 | Producto final del curso validado, documentado, estabilizado y defendido |

## Observabilidad transversal

La observabilidad inicia en S2, no en S10.

En cada sesion se verifica, segun aplique:

- Health checks.
- Logs.
- Config Server.
- Eureka.
- Gateway.
- Base de datos.
- Kafka UI.
- Metricas.
- Evidencia de errores y recuperacion.

S10 consolida estos elementos en una vista operativa del sistema completo.

## Plantilla de cada sesion

Cada sesion usa la misma estructura:

```text
1. Ubicacion en el curso
2. Proposito
3. Resultado de aprendizaje
4. Producto de sesion
5. Concepto distribuido clave
6. Implementacion en el proyecto
7. Pasos para construir el producto de sesion
8. Archivos involucrados
9. Comandos de ejecucion
10. Verificacion funcional
11. Observabilidad y diagnostico
12. Verificacion de base de datos
13. Evidencia esperada
14. Errores frecuentes
15. Preguntas de defensa
16. Checklist de cierre
```

## Criterio de cierre por sesion

Una sesion esta cerrada cuando el estudiante puede mostrar evidencias concretas:

- Salida de comandos.
- Servicio registrado.
- Endpoint funcionando.
- Registro en base de datos.
- Evento Kafka.
- Log o metrica.
- Pantalla Angular.
- Respuesta a preguntas de defensa.
