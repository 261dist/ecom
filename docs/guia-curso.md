# Guía metodológica para sesiones

Esta página no reemplaza al inicio ni al sílabo. Su función es servir como criterio común para redactar, revisar y mantener las sesiones del curso en `docs/sesiones`.

Uso principal:

- Docente: mantener una misma secuencia metodológica en todas las sesiones.
- Estudiante: entender cómo leer cada sesión.
- Mantenimiento de la documentación: evitar duplicaciones entre sesiones, referencias y README de servicios.

## Estructura base de una sesión

Cada sesión debe seguir esta estructura:

```text
1. Introducción
   1.1 Propósito
   1.2 Resultado de aprendizaje
   1.3 Producto de sesión
   1.4 Motivacion de la sesión
   1.5 Ubicación en el curso

2. Explica
   2.1 Conceptos clave
   2.2 Arquitectura del producto en ecom
   2.3 Observabilidad y diagnóstico

3. Aplica: actividad práctica guiada

4. Crea: actividad autónoma

5. Cierre evaluativo
```

## Criterio didáctico

La sesión debe responder claramente:

1. Qué problema práctico motiva el trabajo?
2. Qué producto se construira?
3. Qué componentes intervienen?
4. Cómo se conectan?
5. Cómo se ejecuta en DEV?
6. Cómo se valida en PROD local cuando aplique?
7. Cómo se sabe qué salió bien?
8. Qué evidencia individual debe presentar cada estudiante?

## Programación de laboratorio

Cada sesión presencial dura 4h. La actividad autónoma dura 4h fuera del aula.

Distribución sugerida para el aula:

| Bloque | Tiempo | Función |
|---|---:|---|
| Enlace didáctico | 40 min | En S01: socializacion del sílabo y apertura del curso. Desde S02: cierre breve de evidencias anteriores, bloqueos comunes y apertura de la sesión actual. |
| Explica | 15 min | Conceptos mínimos, arquitectura y flujo de trabajo necesarios para construir. |
| Aplica | 3h | Construcción guiada del producto de sesión, pruebas, errores controlados y verificación técnica. |
| Encargo autónomo | 5 min | Recordar plantilla PDF, evidencias esperadas, criterios mínimos y fecha de entrega. |

Distribución fuera del aula:

| Bloque | Tiempo | Función |
|---|---:|---|
| Crea | 4h | Aplicar el avance de la sesión al proyecto de fin de curso, evidenciar aporte individual, documentar en MkDocs o una herramienta equivalente y dejar trazabilidad en GitHub. |

El cierre evaluativo de la sesión N se revisa al inicio de la sesión N+1 dentro del bloque de enlace didáctico. No se agrega tiempo extra al laboratorio.

La actividad autónoma no debe quedar como una tarea aislada. Cada sesión aporta un artefacto, configuración, validación o evidencia al proyecto de fin de curso. Como el trabajo se realiza en equipo, el producto de cada unidad se construye integrando los productos de sesión aportados por todos los integrantes. Cada integrante puede trabajar en su rama, pero la evaluación revisa que esos aportes hayan sido integrados en una rama común del equipo, con evidencia de merge, resolución de conflictos si aplica, ejecución del sistema integrado y trazabilidad individual en GitHub y en los anexos de la documentación.

Todo PDF solicitado en el trabajo autónomo debe generarse como impresion o exportacion de la documentación correspondiente, elaborada en MkDocs o una herramienta equivalente. La documentación debe publicarse como sitio navegable, por ejemplo en GitHub Pages (`github.io`) u otra plataforma equivalente. No se debe armar un PDF manual separado de la documentación del proyecto.

En los documentos de cada sesión no se repite esta programación. La estructura del archivo se mantiene limpia: introducción, explica, aplica, crea y cierre evaluativo.

## Comandos

Cuando un comando es identico en Windows, macOS y Linux, se documenta en un solo bloque:

```text
PowerShell / bash macOS/Linux
```

Solo se separan bloques cuando cambia la sintaxis, por ejemplo `Invoke-RestMethod` frente a `curl`.

## DEV y PROD local

El curso prioriza ejecución reproducible:

- En DEV, la aplicación normalmente corre con Maven en el host y sus dependencias se levantan con Docker.
- En PROD local, la aplicación se empaqueta y ejecuta como contenedor cuando la sesión lo requiera.
- Si la aplicación corre fuera de Docker, se conecta a dependencias por `localhost:<puerto-expuesto>`.
- Si la aplicación corre dentro de Docker, se conecta a dependencias por `nombre-servicio:<puerto-interno>`.

## Observabilidad transversal

La observabilidad aparece desde la primera sesión como práctica de diagnóstico:

- Logs de arranque.
- Health checks.
- Métricas cuando Actuator lo permita.
- Estado de base de datos.
- Registro de servicios cuando aplique.
- Gateway y balanceo cuando aplique.
- Eventos y trazabilidad cuando aplique.

S10 consolida estos elementos en una vista operativa del sistema completo.

## Cierre evaluativo

El cierre evaluativo se apoya en la evidencia individual entregada después de la actividad autónoma. Una sesión queda cerrada cuando el estudiante puede mostrar:

- Comandos ejecutados.
- Servicio funcionando.
- Endpoint probado.
- Registro en base de datos cuando aplique.
- Health, logs o métricas.
- Evidencia de ejecución DEV y PROD local cuando aplique.
- Respuesta a preguntas de defensa.
- Aporte individual al producto.
