# S11 - Integracion frontend con Angular y Gateway

## Ubicacion en el curso

- Unidad: U2 - Sistema distribuido robusto e integrado.
- Producto de unidad: Sistema distribuido seguro, resiliente, observable, orientado a eventos e integrado con frontend.
- Avance del producto en esta sesion: frontend integrado con Gateway, seguridad y CRUD.

## Proposito

Conectar Angular al sistema distribuido usando Gateway como unica puerta de entrada.

## Resultado de aprendizaje

El estudiante integra login, interceptor JWT, rutas protegidas y CRUD contra microservicios.

## Producto de sesion

`ecom-ng` consume Gateway DEV, permite login y ejecuta CRUD de categorias/productos.

## Concepto distribuido clave

El cliente no debe conocer todos los microservicios. El Gateway protege y simplifica el acceso.

## Implementacion en el proyecto

Angular usa `environment.apiBaseUrl` con `http://localhost:18080`.

## Pasos para construir el producto de sesion

1. Crear o revisar el proyecto Angular.
2. Centralizar la URL del Gateway en `environment.ts`.
3. Crear un servicio base para construir URLs de API.
4. Implementar pantalla de login.
5. Guardar el token obtenido desde `auth-ms`.
6. Crear interceptor para enviar `Authorization: Bearer`.
7. Proteger rutas con guard.
8. Implementar CRUD consumiendo Gateway y validar CORS.

## Archivos involucrados

| Archivo | Proposito |
|---|---|
| `clients/ecom-ng/src/environments/environment.ts` | URL base Gateway |
| `clients/ecom-ng/src/app/core/auth/*` | Auth, guard, interceptor |
| `clients/ecom-ng/src/app/productos/*` | CRUD productos |
| `clients/ecom-ng/src/app/categorias/*` | CRUD categorias |

## Comandos de ejecucion

### PowerShell

```powershell
cd clients/ecom-ng
npm install
npm start
```

### bash macOS/Linux

```bash
cd clients/ecom-ng
npm install
npm start
```

## Verificacion funcional

```text
http://localhost:4200
```

Probar login, categorias y productos.

## Observabilidad y diagnostico

- DevTools del navegador.
- Network requests hacia Gateway.
- Logs de Gateway.
- Logs de `auth-ms`, `catalogo-ms`, `producto-ms`.
- CORS en Gateway si falla el navegador.

## Verificacion de base de datos

```powershell
docker exec -it ecom-postgres-catalogo-dev psql -U ecom -d ecom_catalogo_db -c "SELECT * FROM categorias;"
docker exec -it ecom-postgres-producto-dev psql -U ecom -d ecom_producto_db -c "SELECT * FROM productos;"
```

## Evidencia esperada

- Pantalla Angular funcionando.
- Login exitoso.
- CRUD probado.
- Requests saliendo al Gateway.

## Errores frecuentes

| Problema | Causa probable | Solucion |
|---|---|---|
| CORS | Gateway no permite origen | Revisar config CORS |
| 401 | Token no enviado | Revisar interceptor |
| API no responde | Gateway o servicio apagado | Revisar health y Eureka |

## Preguntas de defensa

1. Por que Angular consume Gateway?
2. Que hace el interceptor?
3. Como se protege una ruta frontend?

## Checklist de cierre

- [ ] Angular levanta.
- [ ] Login funciona.
- [ ] CRUD funciona.
- [ ] Evidencia en BD.
