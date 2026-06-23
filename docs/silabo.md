# Sílabo detallado

Esta página complementa el [sílabo resumido](index.md). Aqui se precisan metodologia, evaluación, evidencias y alcance del curso.

## Enfoque metodológico

El curso se desarrolla como construcción incremental de un producto. Cada sesión parte de una situacion problema, introduce un concepto distribuido, construye un avance verificable y exige evidencia técnica individual.

La evaluación se concentra en cuatro capacidades:

- Implementar.
- Ejecutar.
- Diagnosticar.
- Defender técnicamente.

## Carga de trabajo

Cada sesión tiene una dedicacion esperada de 8 horas:

- 4 horas de laboratorio guiado.
- 4 horas de trabajo fuera del aula.

El laboratorio se usa para construir el avance principal. El trabajo fuera del aula se usa para completar, documentar, probar, inspeccionar evidencias y preparar defensa.

## Criterios de evaluación

La evaluación del producto es grupal, pero la nota es individual. Cada integrante debe evidenciar su aporte mediante código, configuración, comandos ejecutados, registros en base de datos, logs, eventos, capturas, commits, explicación oral o corrección técnica durante la defensa.

Principio de evaluación:

> El producto se construye en equipo; la competencia se demuestra individualmente.

## Evidencias individuales

Cada estudiante debe presentar evidencias asociadas a su participación:

- Código, configuración o documentación propia.
- Comando de prueba ejecutado y explicado.
- Registro en base de datos, evento, log o métrica relacionado con su aporte.
- Commit, issue, tarea o bitacora de responsabilidad.
- Respuesta técnica durante la defensa.
- Corrección o ajuste en vivo cuando el docente lo solicite.

## Evidencias transversales del producto

- Servicio ejecutando.
- Endpoint probado.
- Configuración consultable.
- Registro dinamico del servicio.
- Ruta por punto único de acceso.
- Prueba de escalado o distribución de carga.
- Comunicación entre servicios.
- Escenario de fallo diagnosticado.
- Token o regla de acceso verificada.
- Evento publicado y consumido.
- Estado consistente o compensado.
- Registro en base de datos.
- Log, health, métrica o dashboard.
- Participación individual sustentada.

## Alcance tecnologico

En el sílabo se nombran capacidades y conceptos generales. El stack concreto se desarrolla en las sesiones del proyecto `ecom`.

El curso trabaja producción local con Docker. Kubernetes puede desarrollarse como extension de U3 en entorno local, por ejemplo con Minikube, Kind o Docker Desktop Kubernetes. El despliegue en nube queda fuera del alcance de este curso.

## Convención de trabajo

- Windows: PowerShell.
- macOS/Linux: bash con `curl`.
- Pruebas de API: shell contra el Gateway, no Postman como dependencia obligatoria.
- Swagger: solo directo al puerto asignado de cada microservicio.
- Observabilidad: eje transversal desde S2, consolidado en S10.
