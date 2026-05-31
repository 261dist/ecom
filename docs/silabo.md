# Silabo detallado

Esta pagina complementa el [silabo resumido](index.md). Aqui se precisan metodologia, evaluacion, evidencias y alcance del curso.

## Enfoque metodologico

El curso se desarrolla como construccion incremental de un producto. Cada sesion parte de una situacion problema, introduce un concepto distribuido, construye un avance verificable y exige evidencia tecnica individual.

La evaluacion se concentra en cuatro capacidades:

- Implementar.
- Ejecutar.
- Diagnosticar.
- Defender tecnicamente.

## Carga de trabajo

Cada sesion tiene una dedicacion esperada de 8 horas:

- 4 horas de laboratorio guiado.
- 4 horas de trabajo fuera del aula.

El laboratorio se usa para construir el avance principal. El trabajo fuera del aula se usa para completar, documentar, probar, inspeccionar evidencias y preparar defensa.

## Criterios de evaluacion

La evaluacion del producto es grupal, pero la nota es individual. Cada integrante debe evidenciar su aporte mediante codigo, configuracion, comandos ejecutados, registros en base de datos, logs, eventos, capturas, commits, explicacion oral o correccion tecnica durante la defensa.

Principio de evaluacion:

> El producto se construye en equipo; la competencia se demuestra individualmente.

## Evidencias individuales

Cada estudiante debe presentar evidencias asociadas a su participacion:

- Codigo, configuracion o documentacion propia.
- Comando de prueba ejecutado y explicado.
- Registro en base de datos, evento, log o metrica relacionado con su aporte.
- Commit, issue, tarea o bitacora de responsabilidad.
- Respuesta tecnica durante la defensa.
- Correccion o ajuste en vivo cuando el docente lo solicite.

## Evidencias transversales del producto

- Servicio ejecutando.
- Endpoint probado.
- Configuracion consultable.
- Registro dinamico del servicio.
- Ruta por punto unico de acceso.
- Prueba de escalado o distribucion de carga.
- Comunicacion entre servicios.
- Escenario de fallo diagnosticado.
- Token o regla de acceso verificada.
- Evento publicado y consumido.
- Estado consistente o compensado.
- Registro en base de datos.
- Log, health, metrica o dashboard.
- Participacion individual sustentada.

## Alcance tecnologico

En el silabo se nombran capacidades y conceptos generales. El stack concreto se desarrolla en las sesiones del proyecto `ecom`.

El curso trabaja produccion local con Docker. Kubernetes puede desarrollarse como extension de U3 en entorno local, por ejemplo con Minikube, Kind o Docker Desktop Kubernetes. El despliegue en nube queda fuera del alcance de este curso.

## Convencion de trabajo

- Windows: PowerShell.
- macOS/Linux: bash con `curl`.
- Pruebas de API: shell contra el Gateway, no Postman como dependencia obligatoria.
- Swagger: solo directo al puerto asignado de cada microservicio.
- Observabilidad: eje transversal desde S2, consolidado en S10.
