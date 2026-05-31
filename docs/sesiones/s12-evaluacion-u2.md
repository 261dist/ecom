# S12 - Evaluacion Unidad 2

## Ubicacion en el curso

- Unidad: U2 - Sistema distribuido robusto e integrado.
- Producto de unidad: Sistema distribuido seguro, resiliente, observable, orientado a eventos e integrado con frontend.
- Avance del producto en esta sesion: evaluacion integrada del producto U2.

## Proposito

Validar que el sistema no solo funciona, sino que resiste fallos, protege rutas, emite eventos y se integra con frontend.

## Resultado de aprendizaje

El estudiante demuestra competencias de integracion, seguridad, resiliencia, eventos y diagnostico.

## Producto de sesion

Producto U2 validado en condiciones reales.

## Concepto distribuido clave

La robustez se demuestra bajo escenarios de fallo y verificacion cruzada, no solo con una ruta feliz.

## Implementacion en el proyecto

No se agrega tecnologia nueva. Se integra S6-S11.

## Pasos para construir el producto de sesion

1. Preparar el orden de arranque completo del sistema.
2. Crear datos iniciales necesarios para las pruebas.
3. Ejecutar pruebas de seguridad.
4. Ejecutar pruebas de Feign.
5. Ejecutar pruebas de Circuit Breaker.
6. Ejecutar pruebas Kafka.
7. Ejecutar pruebas desde Angular.
8. Registrar evidencias y explicar diagnostico de fallos.

## Archivos involucrados

Todo el sistema `ecom`.

## Comandos de ejecucion

### PowerShell

Se usan los comandos de cada README de microservicio y de Kafka.

### bash macOS/Linux

Se usan los bloques `Prueba rapida con bash macOS/Linux`.

## Verificacion funcional

- Login.
- CRUD.
- Feign.
- Circuit Breaker.
- Kafka.
- Observabilidad.
- Angular.

## Observabilidad y diagnostico

El estudiante debe explicar que revisa ante:

- 401.
- 503.
- Evento no consumido.
- Servicio no registrado.
- Error de base de datos.

## Verificacion de base de datos

Debe verificar registros en al menos tres bases: auth, catalogo/producto y orden/pago.

## Evidencia esperada

- Salidas de comandos.
- Capturas de Eureka, Angular y Kafka UI.
- Evidencia de BD.
- Logs o metricas.

## Errores frecuentes

| Problema | Causa probable | Solucion |
|---|---|---|
| Sistema incompleto | Servicio faltante | Levantar por orden |
| Demo no reproducible | Falta documentacion | Usar README |

## Preguntas de defensa

1. Como fluye una peticion desde Angular hasta BD?
2. Como se valida seguridad?
3. Como se evidencia Kafka?
4. Como se diagnostica un fallo?

## Checklist de cierre

- [ ] Producto U2 levantado.
- [ ] Evidencias presentadas.
- [ ] Fallo simulado.
- [ ] Respuestas tecnicas sustentadas.
