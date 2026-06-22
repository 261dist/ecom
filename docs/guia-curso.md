# Guia metodologica para sesiones

Esta pagina no reemplaza al inicio ni al silabo. Su funcion es servir como criterio comun para redactar, revisar y mantener las sesiones del curso en `docs/sesiones`.

Uso principal:

- Docente: mantener una misma secuencia metodologica en todas las sesiones.
- Estudiante: entender como leer cada sesion.
- Mantenimiento de la documentacion: evitar duplicaciones entre sesiones, referencias y README de servicios.

## Estructura base de una sesion

Cada sesion debe seguir esta estructura:

```text
1. Introduccion
   1.1 Proposito
   1.2 Resultado de aprendizaje
   1.3 Producto de sesion
   1.4 Motivacion de la sesion
   1.5 Ubicacion en el curso

2. Explica
   2.1 Conceptos clave
   2.2 Arquitectura del producto en ecom
   2.3 Observabilidad y diagnostico

3. Aplica: actividad practica guiada

4. Crea: actividad autonoma

5. Cierre evaluativo
```

## Criterio didactico

La sesion debe responder claramente:

1. Que problema practico motiva el trabajo?
2. Que producto se construira?
3. Que componentes intervienen?
4. Como se conectan?
5. Como se ejecuta en DEV?
6. Como se valida en PROD local cuando aplique?
7. Como se sabe que salio bien?
8. Que evidencia individual debe presentar cada estudiante?

## Programacion de laboratorio

Cada sesion presencial dura 4h. La actividad autonoma dura 4h fuera del aula.

Distribucion sugerida para el aula:

| Bloque | Tiempo | Funcion |
|---|---:|---|
| Enlace didactico | 40 min | En S01: socializacion del silabo y apertura del curso. Desde S02: cierre breve de evidencias anteriores, bloqueos comunes y apertura de la sesion actual. |
| Explica | 15 min | Conceptos minimos, arquitectura y flujo de trabajo necesarios para construir. |
| Aplica | 3h | Construccion guiada del producto de sesion, pruebas, errores controlados y verificacion tecnica. |
| Encargo autonomo | 5 min | Recordar plantilla PDF, evidencias esperadas, criterios minimos y fecha de entrega. |

Distribucion fuera del aula:

| Bloque | Tiempo | Funcion |
|---|---:|---|
| Crea | 4h | Aplicar el avance de la sesion al proyecto de fin de curso, evidenciar aporte individual, documentar en MkDocs y dejar trazabilidad en GitHub. |

El cierre evaluativo de la sesion N se revisa al inicio de la sesion N+1 dentro del bloque de enlace didactico. No se agrega tiempo extra al laboratorio.

La actividad autonoma no debe quedar como una tarea aislada. Cada sesion aporta un artefacto, configuracion, validacion o evidencia al proyecto de fin de curso. Como el trabajo se realiza en equipo, el producto de cada unidad se construye integrando los productos de sesion aportados por todos los integrantes. Cada integrante puede trabajar en su rama, pero la evaluacion revisa que esos aportes hayan sido integrados en una rama comun del equipo, con evidencia de merge, resolucion de conflictos si aplica, ejecucion del sistema integrado y trazabilidad individual en GitHub y en los anexos de MkDocs.

En los documentos de cada sesion no se repite esta programacion. La estructura del archivo se mantiene limpia: introduccion, explica, aplica, crea y cierre evaluativo.

## Comandos

Cuando un comando es identico en Windows, macOS y Linux, se documenta en un solo bloque:

```text
PowerShell / bash macOS/Linux
```

Solo se separan bloques cuando cambia la sintaxis, por ejemplo `Invoke-RestMethod` frente a `curl`.

## DEV y PROD local

El curso prioriza ejecucion reproducible:

- En DEV, la aplicacion normalmente corre con Maven en el host y sus dependencias se levantan con Docker.
- En PROD local, la aplicacion se empaqueta y ejecuta como contenedor cuando la sesion lo requiera.
- Si la aplicacion corre fuera de Docker, se conecta a dependencias por `localhost:<puerto-expuesto>`.
- Si la aplicacion corre dentro de Docker, se conecta a dependencias por `nombre-servicio:<puerto-interno>`.

## Observabilidad transversal

La observabilidad aparece desde la primera sesion como practica de diagnostico:

- Logs de arranque.
- Health checks.
- Metricas cuando Actuator lo permita.
- Estado de base de datos.
- Registro de servicios cuando aplique.
- Gateway y balanceo cuando aplique.
- Eventos y trazabilidad cuando aplique.

S10 consolida estos elementos en una vista operativa del sistema completo.

## Cierre evaluativo

El cierre evaluativo se apoya en la evidencia individual entregada despues de la actividad autonoma. Una sesion queda cerrada cuando el estudiante puede mostrar:

- Comandos ejecutados.
- Servicio funcionando.
- Endpoint probado.
- Registro en base de datos cuando aplique.
- Health, logs o metricas.
- Evidencia de ejecucion DEV y PROD local cuando aplique.
- Respuesta a preguntas de defensa.
- Aporte individual al producto.
