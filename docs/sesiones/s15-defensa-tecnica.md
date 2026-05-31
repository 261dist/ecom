# S15 - Defensa tecnica del producto

## Ubicacion en el curso

- Unidad: U3 - Consolidacion y validacion del producto del curso.
- Producto de unidad: Producto final del curso validado, documentado, estabilizado y defendido.
- Avance del producto en esta sesion: defensa grupal obligatoria.

## Proposito

Sustentar tecnicamente el producto construido durante el curso.

## Resultado de aprendizaje

El grupo demuestra dominio de arquitectura, operacion, diagnostico y decisiones tecnicas.

## Producto de sesion

Defensa tecnica grupal del sistema distribuido.

## Concepto distribuido clave

La defensa valida que el sistema fue comprendido, no solo ensamblado.

## Implementacion en el proyecto

No se implementa nueva funcionalidad. Se demuestra el producto.

## Pasos para construir el producto de sesion

1. Preparar una demo reproducible.
2. Asignar partes de defensa a cada integrante.
3. Preparar explicacion de arquitectura.
4. Preparar evidencias de cada componente.
5. Ejecutar el flujo principal del producto.
6. Simular al menos un fallo o explicar como se diagnostica.
7. Responder preguntas individuales.
8. Registrar observaciones para mejora final.

## Archivos involucrados

Todo el producto y sus evidencias.

## Comandos de ejecucion

El grupo debe ejecutar su demo con PowerShell o bash, segun su entorno.

## Verificacion funcional

La demo debe incluir:

- Login.
- CRUD.
- Feign.
- Circuit Breaker o fallo controlado.
- Kafka.
- Observabilidad.
- BD.

## Observabilidad y diagnostico

Durante la defensa se puede pedir revisar:

- Logs.
- Eureka.
- Kafka UI.
- BD.
- Health.

## Verificacion de base de datos

El grupo debe mostrar registros creados por la demo.

## Evidencia esperada

- Demo funcional.
- Explicacion de arquitectura.
- Respuestas individuales.
- Evidencias tecnicas.

## Errores frecuentes

| Problema | Causa probable | Solucion |
|---|---|---|
| Solo habla un integrante | Falta dominio individual | Preguntas individuales |
| Demo depende de datos ocultos | No hay scripts claros | Usar comandos README |

## Preguntas de defensa

1. Expliquen el flujo completo desde Angular hasta BD.
2. Que ocurre si `catalogo-ms` cae?
3. Como se valida el JWT?
4. Como se evidencia Kafka?
5. Como escalarian el sistema?

## Checklist de cierre

- [ ] Demo ejecutada.
- [ ] Todos los integrantes responden.
- [ ] Arquitectura defendida.
- [ ] Evidencias presentadas.
