# S7 - Seguridad distribuida y control de acceso

## 1. Introduccion

Tiempo: 20 min.

### 1.1 Proposito

Proteger el sistema distribuido mediante autenticacion, autorizacion y validacion de acceso en rutas expuestas por Gateway y microservicios.

### 1.2 Resultado de aprendizaje

El estudiante implementa un flujo de acceso seguro, obtiene un token, consume rutas protegidas y evidencia respuestas 401/403 cuando corresponde.

### 1.3 Producto de sesion

Sistema con `auth-ms` operativo, token de acceso emitido y rutas protegidas en Gateway y microservicios.

### 1.4 Motivacion de la sesion

Un sistema distribuido no debe confiar en cualquier solicitud. La identidad del usuario y sus permisos deben viajar de forma verificable entre cliente, Gateway y servicios internos.

### 1.5 Ubicacion en el curso

- Unidad: U2 - Sistema distribuido robusto.
- Producto de unidad: sistema distribuido seguro, resiliente, consistente, observable e integrado con cliente frontend.
- Avance del producto en esta sesion: autenticacion, autorizacion y proteccion de rutas.

## 2. Explica

Tiempo: 15 min.

### 2.1 Conceptos clave

- Autenticacion.
- Autorizacion.
- Token de acceso.
- Claims.
- Rutas publicas y protegidas.
- Validacion en Gateway y microservicios.

### 2.2 Arquitectura del producto en `ecom`

```mermaid
flowchart LR
    Cliente["Cliente"]
    Gateway["Gateway"]
    Auth["auth-ms"]
    Catalogo["catalogo-ms"]
    Producto["producto-ms"]

    Cliente -->|"login"| Auth
    Auth -->|"token"| Cliente
    Cliente -->|"Bearer token"| Gateway
    Gateway --> Catalogo
    Gateway --> Producto
```

### 2.3 Observabilidad y diagnostico

Revisar health de `auth-ms`, logs de autenticacion, respuesta 401 sin token, respuesta 403 sin permisos y consumo correcto con token.

## 3. Aplica: actividad practica guiada

Tiempo: 3h.

### 3.1 Levantar infraestructura y servicios

Levantar Config Server, Eureka, Gateway, `auth-ms` y microservicios protegidos.

### 3.2 Obtener token

PowerShell:

```powershell
$body = @{
  username = "admin"
  password = "admin123"
} | ConvertTo-Json

$response = Invoke-RestMethod -Method Post -Uri "http://localhost:18080/auth/login" -ContentType "application/json" -Body $body
$token = $response.accessToken
```

bash macOS/Linux:

```bash
TOKEN=$(curl -s -X POST http://localhost:18080/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"admin123"}' | jq -r '.accessToken')
```

### 3.3 Probar ruta protegida

PowerShell:

```powershell
Invoke-RestMethod -Method Get -Uri "http://localhost:18080/api/v1/productos" -Headers @{ Authorization = "Bearer $token" }
```

bash macOS/Linux:

```bash
curl -H "Authorization: Bearer $TOKEN" http://localhost:18080/api/v1/productos
```

### 3.4 Probar error esperado sin token

```bash
curl -i http://localhost:18080/api/v1/productos
```

Resultado esperado: respuesta `401`.

### 3.5 Ruta alternativa: clonar y ejecutar a partir del tag final de la sesion

```bash
git clone --branch vs07-seguridad-distribuida https://github.com/261dist/ecom.git ecom-s07
cd ecom-s07
```

## 4. Crea: actividad autonoma

Tiempo: 4h fuera del aula.

### 4.1 Plantilla de evidencia individual

Entrega un PDF:

```text
S07_Equipo##_ApellidoNombre.pdf
```

#### 4.1.1 Datos del estudiante

- Nombre:
- Equipo:
- Sesion: S07 - Seguridad distribuida y control de acceso
- Rol o aporte realizado:
- Link de GitHub:

#### 4.1.2 Trabajo autonomo realizado

1. Obtener token.
2. Consumir ruta protegida.
3. Probar error sin token.
4. Explicar claims o permisos usados.
5. Evidenciar aporte individual.

### 4.2 Criterios minimos de aceptacion

- PDF con nombre correcto.
- Token obtenido.
- Ruta protegida consumida con token.
- Error 401/403 evidenciado.
- Aporte individual verificable.

## 5. Cierre evaluativo

Tiempo: 20 min.

### 5.1 Resultados esperados

- El sistema emite token.
- Gateway o servicios validan acceso.
- Rutas protegidas responden segun autenticacion.

### 5.2 Evidencia del producto de sesion

Entrega individual:

```text
S07_Equipo##_ApellidoNombre.pdf
```

### 5.3 Preguntas de defensa y reflexion

1. Que diferencia hay entre autenticacion y autorizacion?
2. Que contiene un token?
3. Por que una ruta responde 401?
4. Donde conviene validar acceso: Gateway, servicio o ambos?

### 5.4 Rubrica de evaluacion

| Dimension | Peso | 3 - Logro destacado | 2 - Logro | 1 - Proceso | 0 - Inicio | Puntuacion obtenida |
|---|---:|---|---|---|---|---:|
| 1. Autenticacion | 2 | Evidencia login, token y explicacion clara. | Evidencia login y token. | Evidencia parcial. | No evidencia autenticacion. | |
| 2. Autorizacion | 2 | Evidencia rutas protegidas y permisos. | Evidencia ruta protegida. | Evidencia incompleta. | No evidencia autorizacion. | |
| 3. Errores esperados | 2 | Evidencia y explica 401/403. | Evidencia error esperado. | Error poco claro. | No evidencia error. | |
| 4. Integracion con Gateway/MS | 2 | Explica validacion en arquitectura distribuida. | Evidencia integracion funcional. | Integracion parcial. | No evidencia integracion. | |
| 5. Aporte individual | 1 | Aporte claro y verificable. | Aporte identificable. | Aporte general. | No se identifica aporte. | |
| 6. Orden y reflexion | 1 | PDF ordenado y reflexion tecnica clara. | Evidencia suficiente. | Evidencia poco clara. | PDF insuficiente. | |

Puntuacion acumulada = suma de (`Peso` * `Puntuacion obtenida`) = ____.

Nota final = (`Puntuacion acumulada` / 30) * 20 = ____.

Para usar la rubrica con IA, solicita:

```text
Evalua el PDF usando la rubrica de la sesion.
Para cada dimension selecciona la puntuacion obtenida usando la escala Inicio=0, Proceso=1, Logro=2, Logro destacado=3.
Justifica brevemente cada puntuacion.
Calcula la puntuacion acumulada con la formula: suma de (Peso * Puntuacion obtenida).
Calcula la nota final sobre 20 con la formula: (Puntuacion acumulada / 30) * 20.
Indica 2 fortalezas y 2 recomendaciones.
```
