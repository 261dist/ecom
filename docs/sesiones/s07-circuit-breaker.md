# S7 - Resiliencia con Circuit Breaker

## Ubicacion en el curso

- Unidad: U2 - Sistema distribuido robusto e integrado.
- Producto de unidad: Sistema distribuido seguro, resiliente, observable, orientado a eventos e integrado con frontend.
- Avance del producto en esta sesion: tolerancia a fallos en comunicacion entre servicios.

## Proposito

Evitar que una falla de `catalogo-ms` degrade completamente a `producto-ms`.

## Resultado de aprendizaje

El estudiante prueba un fallo controlado y explica fallback, degradacion y estados del circuito.

## Producto de sesion

Circuit Breaker aplicado al flujo de detalle de producto.

## Concepto distribuido clave

Un Circuit Breaker corta llamadas repetidamente fallidas para proteger al sistema y responder de forma degradada.

## Implementacion en el proyecto

Se aplica resiliencia sobre la llamada de `producto-ms` hacia `catalogo-ms`.

## Pasos para construir el producto de sesion

1. Identificar la llamada remota que puede fallar.
2. Agregar dependencia de Resilience4j o Circuit Breaker usada por el proyecto.
3. Definir la politica del circuito: umbral, ventana, timeout y tiempo de espera.
4. Crear un metodo fallback con respuesta controlada.
5. Aplicar el Circuit Breaker al metodo que usa Feign.
6. Probar el flujo con el servicio destino activo.
7. Apagar el servicio destino y repetir la prueba.
8. Registrar evidencia de respuesta degradada y logs del fallo.

## Archivos involucrados

| Archivo | Proposito |
|---|---|
| `services/producto-ms/pom.xml` | Dependencias de resiliencia |
| `services/producto-ms/src/main/java/.../ProductoServiceImpl.java` | Fallback |
| `infra/config/config-repo/producto-ms-dev.yml` | Parametros del circuito |

## Comandos de ejecucion

### PowerShell

```powershell
Invoke-RestMethod -Method Get -Uri "http://localhost:18080/api/v1/productos/detalle/1"
```

Apagar `catalogo-ms` y repetir la prueba.

### bash macOS/Linux

```bash
curl http://localhost:18080/api/v1/productos/detalle/1
```

## Verificacion funcional

Con `catalogo-ms` apagado, el sistema no debe caer completamente. Debe responder error controlado o fallback definido.

## Observabilidad y diagnostico

- Revisar logs de fallback.
- Revisar metricas actuator si estan expuestas.
- Comparar comportamiento con servicio arriba y servicio abajo.

## Verificacion de base de datos

Verificar que el producto exista antes de probar resiliencia.

```powershell
docker exec -it ecom-postgres-producto-dev psql -U ecom -d ecom_producto_db -c "SELECT * FROM productos;"
```

## Evidencia esperada

- Respuesta normal.
- Respuesta degradada.
- Log del fallo.

## Errores frecuentes

| Problema | Causa probable | Solucion |
|---|---|---|
| No se activa fallback | Configuracion incompleta | Revisar anotacion/configuracion |
| Error no controlado | Excepcion no cubierta | Ajustar fallback |

## Preguntas de defensa

1. Que diferencia hay entre timeout y Circuit Breaker?
2. Que significa estado OPEN?
3. Por que resiliencia no equivale a ocultar errores?

## Checklist de cierre

- [ ] Fallo simulado.
- [ ] Fallback observado.
- [ ] Evidencia de logs presentada.
