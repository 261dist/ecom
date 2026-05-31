# S8 - Seguridad distribuida con JWT

## Ubicacion en el curso

- Unidad: U2 - Sistema distribuido robusto e integrado.
- Producto de unidad: Sistema distribuido seguro, resiliente, observable, orientado a eventos e integrado con frontend.
- Avance del producto en esta sesion: autenticacion, token y rutas protegidas.

## Proposito

Proteger recursos del sistema y centralizar validacion de acceso desde el Gateway.

## Resultado de aprendizaje

El estudiante obtiene un JWT, consume rutas protegidas y explica 401, 403 y autorizacion en sistemas distribuidos.

## Producto de sesion

`auth-ms` emite JWT y Gateway valida el token.

## Concepto distribuido clave

La seguridad en el borde evita replicar controles de entrada en cada cliente y permite proteger el sistema desde el punto unico de acceso.

## Implementacion en el proyecto

`auth-ms` autentica. Gateway valida JWT en rutas protegidas.

## Pasos para construir el producto de sesion

1. Crear o revisar `auth-ms` como servicio responsable de autenticacion.
2. Modelar usuarios y roles en la base de datos.
3. Crear inicializador de usuarios para pruebas del curso.
4. Implementar endpoint `/auth/login`.
5. Generar JWT con issuer, expiracion, usuario y roles.
6. Configurar el mismo secreto e issuer en Gateway.
7. Definir rutas publicas y protegidas en Gateway.
8. Probar una ruta protegida sin token y luego con token.

## Archivos involucrados

| Archivo | Proposito |
|---|---|
| `services/auth-ms/src/main/java/.../AuthController.java` | Login |
| `infra/gateway/src/main/java/.../SecurityConfig.java` | Seguridad de Gateway |
| `infra/config/config-repo/auth-ms-dev.yml` | Config JWT |
| `infra/config/config-repo/gateway-dev.yml` | Rutas |

## Comandos de ejecucion

### PowerShell

```powershell
$body = @{ username = "admin"; password = "admin123" } | ConvertTo-Json
$response = Invoke-RestMethod -Method Post -Uri "http://localhost:18080/auth/login" -ContentType "application/json" -Body $body
$token = $response.accessToken
Invoke-RestMethod -Method Get -Uri "http://localhost:18080/api/v1/productos" -Headers @{ Authorization = "Bearer $token" }
```

### bash macOS/Linux

```bash
response=$(curl -s -X POST "http://localhost:18080/auth/login" -H "Content-Type: application/json" -d '{"username":"admin","password":"admin123"}')
token=$(echo "$response" | jq -r '.accessToken')
curl -H "Authorization: Bearer $token" http://localhost:18080/api/v1/productos
```

## Verificacion funcional

Sin token, la ruta protegida debe devolver `401`. Con token valido, debe responder.

## Observabilidad y diagnostico

- Logs de login en `auth-ms`.
- Logs de rechazo o validacion en Gateway.
- Comparar rutas publicas y protegidas.

## Verificacion de base de datos

```powershell
docker exec -it ecom-postgres-auth-dev psql -U ecom -d ecom_auth_db -c "SELECT id, username, enabled FROM users;"
```

## Evidencia esperada

- Token obtenido.
- Ruta protegida fallando sin token.
- Ruta protegida funcionando con token.

## Errores frecuentes

| Problema | Causa probable | Solucion |
|---|---|---|
| 401 con token | Secreto/issuer no coincide | Revisar config de auth y gateway |
| Login falla | Credenciales incorrectas | Usar `admin/admin123` |

## Preguntas de defensa

1. Que contiene un JWT?
2. Por que Gateway valida el token?
3. Diferencia entre autenticacion y autorizacion?

## Checklist de cierre

- [ ] Login probado.
- [ ] Token usado.
- [ ] 401 demostrado.
- [ ] Ruta protegida consumida.
