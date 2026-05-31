# Guia del curso

Esta guia define como se desarrolla cada sesion en la documentacion del proyecto `ecom`.

El [inicio](index.md) contiene la secuencia del curso. El [silabo detallado](silabo.md) contiene metodologia, evaluacion y alcance. Esta pagina se enfoca solo en reglas operativas para construir, probar y documentar las sesiones.

## Plantilla de cada sesion

Cada sesion usa la misma estructura:

```text
1. Ubicacion en el curso
2. Proposito
3. Resultado de aprendizaje
4. Producto de sesion
5. Concepto distribuido clave
6. Implementacion en el proyecto
7. Distribucion de carga: 4h laboratorio + 4h fuera del aula
8. Pasos para construir el producto de sesion
9. Archivos involucrados
10. Comandos de ejecucion
11. Cierre en produccion local con Docker
12. Verificacion funcional
13. Observabilidad y diagnostico
14. Verificacion de base de datos
15. Evidencia esperada
16. Errores frecuentes
17. Preguntas de defensa
18. Checklist de cierre
```

## Comandos

Cuando un comando es identico en Windows, macOS y Linux, se documenta en un solo bloque:

```text
PowerShell / bash macOS/Linux
```

Solo se separan bloques cuando cambia la sintaxis, por ejemplo `Invoke-RestMethod` frente a `curl`.

## Produccion local con Docker

Todas las sesiones se trabajan primero en DEV, normalmente con Maven y bases de datos en Docker. Al cierre de la sesion, cuando aplique, se ejecuta una validacion breve en produccion local con Docker:

- `docker compose up -d --build` para construir y levantar imagenes.
- Health por Gateway o componente correspondiente.
- Explicacion breve de que en Docker los servicios se ejecutan como contenedores, usan red interna, variables de entorno y perfiles `prod`.

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

## Criterio de cierre por sesion

Una sesion esta cerrada cuando el estudiante puede mostrar evidencias concretas:

- Salida de comandos.
- Servicio registrado.
- Endpoint funcionando.
- Registro en base de datos.
- Evento publicado y consumido.
- Log o metrica.
- Pantalla frontend cuando aplique.
- Respuesta a preguntas de defensa.
