# S5 - Evaluacion U1

## 1. Introduccion

Tiempo: 20 min.

### 1.1 Proposito

Validar que el sistema distribuido base construido en la Unidad 1 funciona como un todo y que cada integrante puede sustentar su aporte.

### 1.2 Resultado de aprendizaje

El estudiante demuestra ejecucion, prueba, diagnostico y defensa tecnica de un sistema base con configuracion centralizada, registro de servicios, Gateway y multiples instancias.

### 1.3 Producto de sesion

Producto U1 integrado: Config Server, Eureka, Gateway, microservicios de negocio, bases de datos y multiples instancias.

### 1.4 Motivacion de la sesion

Un sistema distribuido no se evalua por componentes aislados. La evidencia importante es que los componentes se integran, se ejecutan en orden, responden por Gateway y pueden diagnosticarse ante fallos.

Preguntas para los estudiantes:

1. Que evidencia demuestra que el sistema funciona integrado?
2. Que parte del producto puedes defender individualmente?
3. Que revisas cuando una ruta del Gateway falla?

### 1.5 Ubicacion en el curso

- Unidad: U1 - Sistema distribuido base orientado a produccion.
- Producto de unidad: sistema distribuido base funcional, configurable y preparado para multiples instancias.
- Avance del producto en esta sesion: evaluacion integradora de la Unidad 1.

## 2. Explica

Tiempo: 15 min.

### 2.1 Conceptos clave

- **Integracion**: los componentes funcionan coordinadamente.
- **Evidencia individual**: prueba verificable del aporte de cada estudiante.
- **Diagnostico**: capacidad de ubicar fallos en Config Server, Eureka, Gateway, microservicio o BD.

### 2.2 Arquitectura del producto en `ecom`

```mermaid
flowchart TB
    Cliente["Cliente<br/>PowerShell / bash"]
    Gateway["Gateway"]
    Eureka["Eureka"]
    Config["Config Server"]
    Catalogo["catalogo-ms"]
    Producto["producto-ms"]
    DB1["ecom_catalogo_db"]
    DB2["ecom_producto_db"]

    Cliente --> Gateway
    Gateway -. descubre servicios .-> Eureka
    Catalogo -. registra instancia .-> Eureka
    Producto -. registra instancia .-> Eureka
    Gateway --> Catalogo
    Gateway --> Producto
    Catalogo -. carga configuracion .-> Config
    Producto -. carga configuracion .-> Config
    Catalogo --> DB1
    Producto --> DB2
```

### 2.3 Observabilidad y diagnostico

Senales obligatorias:

- Config Server entrega perfiles.
- Eureka muestra servicios registrados.
- Gateway responde health.
- CRUD responde por Gateway.
- BD contiene registros.
- Se evidencia mas de una instancia cuando corresponde.

## 3. Aplica: actividad practica guiada

Tiempo: 3h.

En esta sesion se realiza una evaluacion practica. El equipo levanta el sistema y cada integrante evidencia su aporte individual.

### 3.1 Preparar orden de arranque

Orden recomendado:

1. Config Server.
2. Eureka.
3. Gateway.
4. Bases de datos.
5. Microservicios.
6. Segunda instancia, si aplica.

### 3.2 Ejecutar pruebas base

PowerShell / bash macOS/Linux:

```bash
curl http://localhost:18888/catalogo-ms/dev
curl http://localhost:18761
curl http://localhost:18080/actuator/health
curl http://localhost:18080/api/v1/categorias
```

### 3.3 Validar multiples instancias

Verificar en Eureka que el servicio tiene mas de una instancia o explicar por que no se pudo levantar.

### 3.4 Inspeccionar base de datos

PowerShell / bash macOS/Linux:

```bash
docker exec -it ecom-postgres-catalogo-dev psql -U ecom -d ecom_catalogo_db -c "SELECT * FROM categorias;"
```

### 3.5 Demostracion individual

Cada integrante debe poder responder:

- Que parte implemento.
- Que archivo modifico.
- Que prueba ejecuto.
- Que error diagnostico.

## 4. Crea: actividad autonoma

Tiempo: 4h fuera del aula.

### 4.1 Plantilla de evidencia individual

Entrega un PDF con el siguiente nombre:

```text
S05_Equipo##_ApellidoNombre.pdf
```

#### 4.1.1 Datos del estudiante

- Nombre:
- Equipo:
- Sesion: S05 - Evaluacion U1
- Rol o aporte realizado:
- Link de GitHub:

#### 4.1.2 Trabajo autonomo realizado

1. Ordenar evidencias de U1.
2. Corregir observaciones detectadas.
3. Completar README o documentacion del modulo asignado.
4. Preparar defensa individual.
5. Registrar comandos y resultados.

#### 4.1.3 Evidencia tecnica

- Config Server.
- Eureka.
- Gateway.
- CRUD por Gateway.
- BD con registros.
- Multiples instancias.
- Aporte individual.

#### 4.1.4 Error o hallazgo

Describe un problema de integracion y como lo diagnosticarias.

#### 4.1.5 Reflexion tecnica breve

Explica como los componentes de U1 forman un sistema distribuido base.

### 4.2 Criterios minimos de aceptacion

- PDF con nombre correcto.
- Evidencia del producto U1 integrado.
- Evidencia de aporte individual.
- Pruebas por consola.
- Diagnostico tecnico.

## 5. Cierre evaluativo

Tiempo: 20 min.

### 5.1 Resultados esperados

- Producto U1 levantado.
- Pruebas por Gateway ejecutadas.
- Servicios registrados en Eureka.
- Configuracion consultada.
- Cada integrante sustenta su aporte.

### 5.2 Evidencia del producto de sesion

Cada estudiante entrega un PDF individual siguiendo la plantilla de la seccion 4.1.

Nombre del archivo:

```text
S05_Equipo##_ApellidoNombre.pdf
```

### 5.3 Preguntas de defensa y reflexion

1. Cual fue tu aporte concreto en U1?
2. Como se levanta el sistema base?
3. Como se prueba sin Postman?
4. Como sabes que hay multiples instancias?
5. Que revisas si una ruta devuelve 503?

### 5.4 Rubrica de evaluacion

| Dimension | Peso | 3 - Logro destacado | 2 - Logro | 1 - Proceso | 0 - Inicio | Puntuacion obtenida |
|---|---:|---|---|---|---|---:|
| 1. Integracion del producto U1 | 2 | Evidencia sistema completo integrado y funcionando. | Evidencia componentes principales funcionando. | Evidencia parcial de componentes. | No evidencia integracion. | |
| 2. Pruebas tecnicas | 2 | Pruebas por Config, Eureka, Gateway, CRUD y BD completas. | Pruebas principales completas. | Pruebas incompletas o poco claras. | No evidencia pruebas. | |
| 3. Diagnostico | 2 | Diagnostica fallos de integracion con claridad. | Explica un problema y causa probable. | Menciona problema sin analisis. | No diagnostica. | |
| 4. Aporte individual | 2 | Aporte verificable, claro y conectado al producto. | Aporte identificable. | Aporte general. | No se identifica aporte. | |
| 5. Defensa tecnica | 1 | Responde con precision y criterio tecnico. | Responde adecuadamente. | Responde parcialmente. | No sustenta. | |
| 6. Orden y evidencias | 1 | PDF ordenado, completo y legible. | Evidencias suficientes. | Evidencias poco claras. | Evidencia insuficiente. | |

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
