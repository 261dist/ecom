# S13 - Validación end-to-end del producto del curso

## 1. Introducción

Tiempo: 20 min.

### 1.1 Propósito

Validar el producto del curso como sistema completo, desde cliente o shell hasta Gateway, servicios, eventos, base de datos y observabilidad.

### 1.2 Resultado de aprendizaje

El estudiante ejecuta flujos end-to-end, verifica resultados en cada capa y produce evidencias reproducibles.

### 1.3 Producto de sesión

Checklist end-to-end del producto del curso con evidencias por capa.

### 1.4 Motivacion de la sesión

Un sistema distribuido solo se considera completo cuando sus componentes cooperan en un flujo real de negocio y el equipo puede demostrarlo de forma reproducible.

### 1.5 Ubicación en el curso

- Unidad: U3 - Validación y consolidación del producto del curso.
- Producto de unidad: producto final del curso validado, documentado, estabilizado y defendido.
- Avance del producto en esta sesión: validación integral del producto del curso.

## 2. Explica

Tiempo: 15 min.

### 2.1 Conceptos clave

- Validación end-to-end.
- Evidencia reproducible.
- Trazabilidad del flujo.
- Datos finales.
- Diagnóstico por capas.

### 2.2 Arquitectura del producto en `ecom`

En esta sesión se valida el producto completo. El foco no es agregar un componente nuevo, sino demostrar que el flujo atraviesa cliente, Gateway, seguridad, microservicios, eventos, bases de datos y observabilidad.

#### 2.2.1 Validación end-to-end en DEV

```mermaid
flowchart TB
    Cliente["Cliente<br/>PowerShell / bash / ecom-ng"]
    Gateway["Gateway<br/>localhost:18080"]
    Auth["auth-ms<br/>puerto dinamico"]
    Catalogo["catalogo-ms<br/>puerto dinamico"]
    Producto["producto-ms<br/>puerto dinamico"]
    Orden["orden-ms<br/>puerto dinamico"]
    Pago["pago-ms<br/>puerto dinamico"]
    Kafka["Kafka broker<br/>localhost:41092"]
    DB["Bases de datos<br/>PostgreSQL DEV"]
    Obs["Observabilidad<br/>Grafana localhost:13000"]

    Cliente -->|"login + CRUD + orden"| Gateway
    Gateway --> Auth
    Gateway --> Catalogo
    Gateway --> Producto
    Gateway --> Orden
    Orden -->|"orden-eventos"| Kafka
    Kafka --> Pago
    Pago -->|"pago-eventos"| Kafka
    Kafka --> Orden
    Catalogo --> DB
    Producto --> DB
    Orden --> DB
    Pago --> DB
    Auth --> DB
    Gateway -.->|"logs / métricas"| Obs
    Catalogo -.->|"logs / métricas"| Obs
    Producto -.->|"logs / métricas"| Obs
    Orden -.->|"logs / métricas"| Obs
    Pago -.->|"logs / métricas"| Obs
```

#### 2.2.2 Validación end-to-end en PROD local

```mermaid
flowchart TB
    Cliente["Cliente<br/>PowerShell / bash / ecom-ng"]

    subgraph Docker["Docker Networks: ecom-prod-net + ecom-kafka-prod-net + observabilidad"]
        Gateway["ecom-gateway<br/>host localhost:28082"]
        Auth["auth-ms<br/>8080 interno"]
        Catalogo["catalogo-ms<br/>8080 interno"]
        Producto["producto-ms<br/>8080 interno"]
        Orden["orden-ms<br/>8080 interno"]
        Pago["pago-ms<br/>8080 interno"]
        Kafka["Kafka broker<br/>kafka:9092<br/>UI localhost:28085"]
        DB["Bases de datos<br/>PostgreSQL PROD local"]
        Obs["Grafana<br/>localhost:23000"]
    end

    Cliente -->|"login + CRUD + orden"| Gateway
    Gateway --> Auth
    Gateway --> Catalogo
    Gateway --> Producto
    Gateway --> Orden
    Orden -->|"orden-eventos"| Kafka
    Kafka --> Pago
    Pago -->|"pago-eventos"| Kafka
    Kafka --> Orden
    Catalogo --> DB
    Producto --> DB
    Orden --> DB
    Pago --> DB
    Auth --> DB
    Gateway -.->|"logs / métricas"| Obs
    Catalogo -.->|"logs / métricas"| Obs
    Producto -.->|"logs / métricas"| Obs
    Orden -.->|"logs / métricas"| Obs
    Pago -.->|"logs / métricas"| Obs
```

### 2.3 Observabilidad y diagnóstico

Validar cada salto del flujo con logs, métricas, BD, Kafka UI, Eureka, Gateway y respuestas HTTP.

## 3. Aplica: actividad práctica guiada

Tiempo: 3h.

En el laboratorio, el docente guía una validación integral. Cada equipo ejecuta el mismo flujo, registra evidencias por capa y anota incidencias técnicas con causa probable.

### 3.1 Preparar checklist end-to-end

Producto del paso: flujo principal y evidencias esperadas definidas antes de ejecutar.

Checklist mínimo:

- Login.
- CRUD de categoría.
- CRUD de producto.
- Creación de orden.
- Procesamiento de pago.
- Validación en BD.
- Validación en Kafka.
- Validación en logs/métricas.

### 3.2 Definir flujo principal

Ejemplo mínimo:

1. Login.
2. Crear categoría.
3. Crear producto.
4. Crear orden.
5. Procesar pago.
6. Revisar estado final.

### 3.3 Levantar sistema DEV

Producto del paso: sistema completo disponible en desarrollo.

Levantar:

- Config Server.
- Eureka.
- Gateway.
- Kafka.
- Observabilidad.
- Microservicios necesarios.
- Frontend, si se usará en la demo.

### 3.4 Validar health y registro de servicios

Producto del paso: infraestructura base saludable.

Verificar:

PowerShell:

```powershell
Invoke-RestMethod -Method Get -Uri "http://localhost:18080/actuator/health"
```

bash macOS/Linux:

```bash
curl http://localhost:18080/actuator/health
```

Abrir Eureka:

```text
http://localhost:18761
```

### 3.5 Ejecutar login

Producto del paso: token válido para el flujo protegido.

Guardar token si la prueba se realiza desde shell.

### 3.6 Ejecutar CRUD de categoría

Producto del paso: categoría creada y consultable por Gateway.

Evidenciar respuesta HTTP y registro en base de datos.

### 3.7 Ejecutar CRUD de producto

Producto del paso: producto creado con categoría asociada.

Evidenciar respuesta HTTP y validación de relación con categoría.

### 3.8 Ejecutar flujo de orden y pago

Producto del paso: orden creada y pago procesado por eventos.

Usar shell, frontend o ambos, siempre mediante Gateway cuando corresponda.

### 3.9 Verificar resultados por capa

Validar:

- Respuesta HTTP.
- Registro en BD.
- Evento publicado/consumido.
- Logs.
- Métricas o dashboard.

### 3.10 Verificar Kafka UI

Producto del paso: eventos de orden y pago visibles.

Abrir:

```text
http://localhost:41085
```

Revisar `orden-eventos` y `pago-eventos`.

### 3.11 Verificar bases de datos

Producto del paso: datos finales visibles en las tablas de cada microservicio.

Consultar tablas de categorías, productos, ordenes y pagos con `docker exec` y `psql`.

### 3.12 Revisar observabilidad

Producto del paso: evidencias de logs o métricas del flujo.

Revisar:

- Grafana DEV: `http://localhost:13000`
- Prometheus DEV: `http://localhost:19090`
- Loki DEV: `http://localhost:13100`

### 3.13 Registrar incidencias

Documentar errores, causa probable y accion correctiva.

### 3.14 Repetir flujo en PROD local

Producto del paso: flujo principal probado con contenedores.

Levantar infraestructura, Kafka, observabilidad y microservicios con Docker. Usar Gateway PROD:

```text
http://localhost:28082
```

### 3.15 Comparar DEV y PROD local

Producto del paso: diferencias operativas identificadas.

Comparar:

- Puertos.
- URLs.
- Uso de `localhost` vs nombres de servicio Docker.
- Swagger habilitado o deshabilitado.
- Health y logs.

### 3.16 Consolidar evidencia del equipo

Producto del paso: evidencia lista para la revisión de cierre.

Agrupar capturas, comandos, logs y hallazgos. Cada integrante debe identificar su aporte.

### 3.17 Ruta alternativa: clonar y ejecutar a partir del tag final de la sesión

```bash
git clone --branch vs13-validacion-end-to-end https://github.com/261dist/ecom.git ecom-s13
cd ecom-s13
```

## 4. Crea: actividad autónoma

Tiempo: 4h fuera del aula.

Esta actividad autónoma se desarrolla sobre el proyecto de fin de curso del equipo. El producto de la unidad se construye por acumulacion de los avances de cada sesión; por eso, la evidencia de esta sesión debe incorporarse a la documentación del proyecto y quedar trazable en GitHub.

### 4.1 Plantilla de evidencia individual

Entrega un PDF:

El PDF de esta sesión debe generarse como impresion o exportacion de la sección correspondiente en MkDocs o una herramienta equivalente. No se acepta un PDF armado manualmente fuera de la documentación del proyecto.

```text
S13_Equipo##_ApellidoNombre.pdf
```

#### 4.1.1 Datos del estudiante

- Nombre:
- Equipo:
- Sesión: S13 - Validación end-to-end del producto del curso
- Rol o aporte realizado:
- Link de GitHub:

#### 4.1.2 Trabajo autónomo realizado

1. Completar evidencias del flujo end-to-end.
2. Corregir fallos detectados.
3. Registrar datos finales.
4. Documentar aporte individual.
5. Preparar demo final.

### 4.2 Criterios mínimos de aceptación

- PDF con nombre correcto.
- Flujo end-to-end evidenciado.
- Evidencias por capa.
- Incidencias registradas.
- Aporte individual verificable.

## 5. Cierre evaluativo

Tiempo: 20 min.

### 5.1 Resultados esperados

- Flujo completo probado.
- Evidencia de datos y eventos.
- Diagnóstico por capas.
- Incidencias documentadas.

### 5.2 Evidencia del producto de sesión

Entrega individual:

```text
S13_Equipo##_ApellidoNombre.pdf
```

### 5.3 Preguntas de defensa y reflexión

1. Cuál es el flujo end-to-end principal?
2. Dónde se valida seguridad?
3. Dónde ocurre consistencia eventual?
4. Cómo demuestras que el flujo llego a BD?
5. Qué aportaste individualmente a la validación?

### 5.4 Rúbrica de evaluación

| Dimensión | Peso | 3 - Logro destacado | 2 - Logro | 1 - Proceso | 0 - Inicio | Puntuación obtenida |
|---|---:|---|---|---|---|---:|
| 1. Flujo end-to-end | 2 | Evidencia flujo completo y reproducible. | Evidencia flujo principal. | Flujo parcial. | No evidencia flujo. | |
| 2. Evidencias por capa | 2 | Evidencia cliente, Gateway, servicios, eventos y BD. | Evidencia capas principales. | Evidencia incompleta. | No evidencia capas. | |
| 3. Diagnóstico | 2 | Analiza incidencias con causa y solución. | Explica problemas principales. | Menciona incidencias sin análisis. | No diagnostica. | |
| 4. Reproducibilidad | 2 | Comandos y pasos claros para repetir la prueba. | Pasos suficientes. | Pasos incompletos. | No es reproducible. | |
| 5. Aporte individual | 1 | Aporte claro y verificable. | Aporte identificable. | Aporte general. | No se identifica aporte. | |
| 6. Orden y reflexión | 1 | PDF ordenado y reflexión técnica clara. | Evidencia suficiente. | Evidencia poco clara. | PDF insuficiente. | |

Puntuación acumulada = suma de (`Peso` * `Puntuacion obtenida`) = ____.

Nota final = (`Puntuacion acumulada` / 30) * 20 = ____.

Para usar la rúbrica con IA, solicita:

```text
Evalúa el PDF usando la rúbrica de la sesión.
Para cada dimensión selecciona la puntuación obtenida usando la escala Inicio=0, Proceso=1, Logro=2, Logro destacado=3.
Justifica brevemente cada puntuación.
Calcula la puntuación acumulada con la fórmula: suma de (Peso * Puntuación obtenida).
Calcula la nota final sobre 20 con la fórmula: (Puntuación acumulada / 30) * 20.
Indica 2 fortalezas y 2 recomendaciones.
```
