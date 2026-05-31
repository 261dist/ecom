# S13 - Validacion integral del producto del curso

## Ubicacion en el curso

- Unidad: U3 - Consolidacion y validacion del producto del curso.
- Producto de unidad: Producto final del curso validado, documentado, estabilizado y defendido.
- Avance del producto en esta sesion: validacion end-to-end del sistema completo.

## Proposito

Probar el producto del curso como sistema completo, no como piezas aisladas.

## Resultado de aprendizaje

El estudiante ejecuta flujos end-to-end y produce evidencias de integracion.

## Producto de sesion

Checklist end-to-end del producto del curso.

## Concepto distribuido clave

La validacion integral confirma que los servicios cooperan correctamente bajo un flujo de negocio completo.

## Implementacion en el proyecto

Se prueban flujos desde Angular o shell hasta Gateway, microservicios, Kafka y BD.

## Pasos para construir el producto de sesion

1. Definir el flujo end-to-end principal del producto.
2. Preparar datos base.
3. Ejecutar login.
4. Ejecutar operaciones CRUD.
5. Ejecutar flujo con Feign.
6. Ejecutar flujo con Kafka.
7. Verificar resultados en base de datos.
8. Guardar evidencias reproducibles.

## Archivos involucrados

Todo el proyecto.

## Comandos de ejecucion

### PowerShell

Usar README de cada modulo para levantar y probar.

### bash macOS/Linux

Usar bloques `bash macOS/Linux` de los README.

## Verificacion funcional

Flujo minimo:

1. Login.
2. Crear categoria.
3. Crear producto.
4. Consultar detalle.
5. Crear orden.
6. Ver pago generado.

## Observabilidad y diagnostico

- Eureka.
- Gateway.
- Kafka UI.
- Logs.
- BD.
- Angular DevTools.

## Verificacion de base de datos

Debe existir evidencia en categorias, productos, ordenes y pagos.

## Evidencia esperada

- Checklist completado.
- Salidas de comandos.
- Capturas de UI.
- Registros BD.

## Errores frecuentes

| Problema | Causa probable | Solucion |
|---|---|---|
| Pago no aparece | Kafka o consumer apagado | Revisar S9 |
| Producto sin detalle | Categoria no existe | Crear categoria |

## Preguntas de defensa

1. Donde se ve cada evidencia del flujo?
2. Que parte es sincrona y que parte es asincrona?
3. Que componente fallaria si se apaga Eureka?

## Checklist de cierre

- [ ] Flujo completo probado.
- [ ] Evidencias guardadas.
- [ ] Fallos diagnosticados.
