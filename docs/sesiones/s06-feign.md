# S6 - Comunicacion entre microservicios con OpenFeign

## Ubicacion en el curso

- Unidad: U2 - Sistema distribuido robusto e integrado.
- Producto de unidad: Sistema distribuido seguro, resiliente, observable, orientado a eventos e integrado con frontend.
- Avance del producto en esta sesion: comunicacion sincrona entre microservicios.

## Proposito

Implementar una operacion donde un microservicio consulta datos de otro usando su nombre logico.

## Resultado de aprendizaje

El estudiante explica y prueba una llamada entre servicios usando OpenFeign y Eureka.

## Producto de sesion

`producto-ms` consulta informacion de categorias desde `catalogo-ms`.

## Concepto distribuido clave

La comunicacion sincrona permite componer operaciones, pero introduce dependencia temporal entre servicios.

## Implementacion en el proyecto

`producto-ms` usa un cliente Feign para consultar `catalogo-ms`.

## Pasos para construir el producto de sesion

1. Identificar una operacion que requiere datos de otro microservicio.
2. Agregar dependencia de OpenFeign al microservicio consumidor.
3. Habilitar Feign Clients en la aplicacion Spring Boot.
4. Crear una interfaz cliente con el nombre logico del servicio destino.
5. Mapear el endpoint remoto que se necesita consumir.
6. Crear DTOs para no acoplar entidades entre microservicios.
7. Usar el cliente Feign desde la capa de servicio.
8. Probar la operacion por Gateway y revisar logs de ambos servicios.

## Archivos involucrados

| Archivo | Proposito |
|---|---|
| `services/producto-ms/src/main/java/.../CatalogoClient.java` | Cliente Feign |
| `services/producto-ms/src/main/java/.../ProductoServiceImpl.java` | Flujo de negocio |
| `infra/config/config-repo/gateway-dev.yml` | Ruta de productos |

## Comandos de ejecucion

### PowerShell

```powershell
Invoke-RestMethod -Method Get -Uri "http://localhost:18080/api/v1/productos/detalle/1"
```

### bash macOS/Linux

```bash
curl http://localhost:18080/api/v1/productos/detalle/1
```

## Verificacion funcional

El detalle de producto debe incluir informacion relacionada con la categoria.

## Observabilidad y diagnostico

- Logs de `producto-ms`.
- Logs de `catalogo-ms`.
- Eureka confirma ambos servicios registrados.
- Si `catalogo-ms` cae, la llamada sincrona falla o activa resiliencia en S7.

## Verificacion de base de datos

```powershell
docker exec -it ecom-postgres-producto-dev psql -U ecom -d ecom_producto_db -c "SELECT * FROM productos;"
docker exec -it ecom-postgres-catalogo-dev psql -U ecom -d ecom_catalogo_db -c "SELECT * FROM categorias;"
```

## Evidencia esperada

- Endpoint de detalle probado.
- Logs que muestran llamada entre servicios.

## Errores frecuentes

| Problema | Causa probable | Solucion |
|---|---|---|
| Error al consultar categoria | `catalogo-ms` apagado | Levantar y registrar `catalogo-ms` |
| 404 categoria | No existe registro asociado | Crear categoria |

## Preguntas de defensa

1. Que riesgo introduce una llamada sincrona?
2. Por que Feign usa el nombre del servicio?
3. Que pasa si `catalogo-ms` no esta disponible?

## Checklist de cierre

- [ ] Feign probado.
- [ ] Producto y categoria existen.
- [ ] Logs revisados.
