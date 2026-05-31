# S14 - Correccion, evidencias y cierre tecnico

## Ubicacion en el curso

- Unidad: U3 - Consolidacion y validacion del producto del curso.
- Producto de unidad: Producto final del curso validado, documentado, estabilizado y defendido.
- Avance del producto en esta sesion: producto estabilizado y documentado.

## Proposito

Cerrar brechas tecnicas antes de la defensa.

## Resultado de aprendizaje

El estudiante corrige, documenta y prepara evidencias reproducibles.

## Producto de sesion

Producto final listo para defensa.

## Concepto distribuido clave

Un sistema distribuido entregable debe ser reproducible: otra persona debe poder levantarlo y verificarlo.

## Implementacion en el proyecto

Se revisan README, comandos, puertos, perfiles, scripts de prueba y evidencias.

## Pasos para construir el producto de sesion

1. Revisar que cada README coincida con el codigo real.
2. Validar comandos PowerShell.
3. Validar comandos bash macOS/Linux.
4. Revisar puertos DEV y PROD.
5. Revisar perfiles y Config Server.
6. Completar evidencias faltantes.
7. Corregir errores detectados en la validacion integral.
8. Preparar guion de defensa.

## Archivos involucrados

| Archivo | Proposito |
|---|---|
| `README.md` | Onboarding raiz |
| `services/*/README.md` | Operacion por servicio |
| `kafka/README.md` | Operacion Kafka |
| `docs/` | Guia del curso y evidencias |

## Comandos de ejecucion

### PowerShell

Repetir pruebas rapidas de cada README.

### bash macOS/Linux

Repetir bloques `curl`.

## Verificacion funcional

El sistema debe levantarse desde cero siguiendo documentacion.

## Observabilidad y diagnostico

Se documenta que revisar si falla:

- Config.
- Eureka.
- Gateway.
- BD.
- Kafka.
- Frontend.

## Verificacion de base de datos

Cada grupo debe incluir comandos `psql` usados y resultados esperados.

## Evidencia esperada

- README completos.
- Comandos validados.
- Capturas.
- Registro de problemas corregidos.

## Errores frecuentes

| Problema | Causa probable | Solucion |
|---|---|---|
| Documentacion desactualizada | Codigo cambio | Verificar contra compose/config |
| Demo fragil | Orden de arranque incompleto | Crear checklist |

## Preguntas de defensa

1. Como se levanta el sistema desde cero?
2. Que evidencia prueba que el sistema funciona?
3. Que limitaciones tiene la implementacion?

## Checklist de cierre

- [ ] README actualizados.
- [ ] Puertos verificados.
- [ ] Pruebas reproducibles.
- [ ] Evidencias preparadas.
