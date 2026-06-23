# S5 - Evaluación U1

## 1. Instrucciones iniciales

Tiempo: 5 min.

### 1.1 Propósito

Validar que el sistema distribuido base construido en la Unidad 1 funciona como un todo y que cada integrante puede sustentar su aporte.

### 1.2 Resultado de aprendizaje

El estudiante demuestra ejecución, prueba, diagnóstico y defensa técnica de un sistema base con configuración centralizada, registro de servicios, Gateway y múltiples instancias.

### 1.3 Producto de sesión

Producto U1 integrado: Config Server, Eureka, Gateway, microservicios de negocio, bases de datos y múltiples instancias.

### 1.4 Preguntas del docente durante la sustentación

Un sistema distribuido no se evalúa por componentes aislados. La evidencia importante es que los componentes se integran, se ejecutan en orden, responden por Gateway y pueden diagnosticarse ante fallos.

Preguntas que el docente puede realizar a cada estudiante:

1. Qué evidencia demuestra que el sistema funciona integrado?
2. Qué parte del producto puedes defender individualmente?
3. Qué revisas cuando una ruta del Gateway falla?

### 1.5 Ubicación en el curso

- Unidad: U1 - Sistema distribuido base orientado a producción.
- Producto de unidad: sistema distribuido base funcional, configurable y preparado para múltiples instancias.
- Avance del producto en esta sesión: evaluación integradora de la Unidad 1.

## 2. Encuadre de la evaluación

Tiempo: 10 min.

El docente presenta brevemente la arquitectura del producto de unidad, recuerda la distribución de tiempo por equipo y pasa directamente a las exposiciones.

### 2.1 Arquitectura del producto de unidad

```mermaid
flowchart TB
    Cliente["Cliente<br/>PowerShell / bash"]
    Gateway["Gateway"]
    Eureka["Eureka"]
    Config["Config Server"]
    Catalogo["catalogo-ms"]
    Producto["producto-ms"]
    DB1["ecom_catálogo_db"]
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

### 2.2 Tiempo de exposición por equipo

Cada grupo dispone de hasta 18 minutos:

- 10 minutos de exposición del proyecto U1.
- 5 minutos de demo técnica.
- 3 minutos de preguntas del docente a integrantes del equipo.

## 3. Presentación y sustentación del producto

Tiempo: 3h 45 min para la ronda de evaluación de equipos.

En esta sesión se realiza la exposición y evaluación práctica. Cada equipo dispone de hasta 18 minutos para presentar el producto U1, mostrar la demo y responder preguntas. La rúbrica se aplica al cierre de la exposición de cada equipo.

### 3.1 Plantilla de entrega

La evaluación U1 requiere tres entregables:

1. Documentación en MkDocs o herramienta equivalente del avance U1 del proyecto final, organizada por sesiones y con guías reproducibles.
2. PDF grupal de la evaluación generado como impresion o exportacion de la documentación y subido a la plataforma BLearning (BL).
3. Presentación del proyecto U1 (PPT o equivalente) subida a BL.

El link de la documentación debe aparecer en el `index` del PDF. La documentación no presenta productos aislados de sesión: organiza el avance U1 del proyecto final usando S01, S02, S03, S04 y S05 como estructura de evidencias. Para la unidad, el equipo debe juntar e integrar los productos de sesión desarrollados por todos los integrantes en una rama común del equipo. No basta con mostrar ramas o PR separados: debe evidenciarse el merge o integración, la resolución de conflictos si aplica y la ejecución del sistema integrado. Además, el repositorio GitHub debe evidenciar el aporte o participación individual de cada integrante mediante commits, ramas, merges o pull requests de código y documentación. Esa evidencia debe incluirse también en la documentación como anexos, un anexo por integrante, para que al imprimir o exportar el sitio se genere un PDF ordenado. Cada integrante debe mostrar una demo de la parte que trabajó.

El PDF de esta evaluación debe ser la impresion o exportacion directa del sitio de documentación. No se acepta un PDF armado manualmente fuera de la documentación.

Entrega el PDF grupal con el siguiente nombre:

```text
S05_Equipo##_U1_Docs.pdf
```

Entrega la presentación con el siguiente nombre:

```text
U1_Equipo##_Presentación.pdf
```

La documentación debe estar en el repositorio GitHub y publicarse como sitio navegable, por ejemplo en GitHub Pages (`github.io`) u otra plataforma equivalente. Si usan MkDocs, también pueden verificarla localmente con `mkdocs serve`.

#### 3.1.1 Datos del equipo

- Equipo:
- Sesión: S05 - Evaluación U1
- Proyecto:
- Link de GitHub:
- Link de documentación:
- Rama integrada evaluada:
- Evidencia de integración o merge:
- Integrantes:
- Productos de sesión integrados por el equipo:
- Anexos individuales incluidos:

#### 3.1.2 Evidencia técnica del avance U1

- Config Server.
- Eureka.
- Gateway.
- CRUD por Gateway.
- BD con registros.
- Múltiples instancias.
- Avance del proyecto final correspondiente a U1.

#### 3.1.3 Presentación del proyecto U1

La presentación debe incluir:

- Nombre del proyecto y equipo.
- Arquitectura U1.
- Flujo de ejecución.
- Evidencias principales.
- Aporte individual de cada integrante.
- Evidencia de participación individual de cada integrante en GitHub.
- Demo asignada a cada integrante.
- Problemas encontrados y decisiones técnicas.

#### 3.1.4 Documentación en MkDocs o herramienta equivalente

La documentación debe seguir una estructura ordenada por sesión y anexos. Cada sesión documenta el avance del proyecto final que corresponde a esa etapa y debe integrar los aportes realizados por los integrantes del equipo:

- S01: microservicio base y CRUD.
- S02: Config Server y perfiles `dev` / `prod`.
- S03: Eureka y registro de servicios.
- S04: Gateway, rutas y balanceo.
- S05: integración y evaluación U1.
- Anexos: evidencia de participación individual, un anexo por integrante.

Cada guía debe contener comandos, puertos, rutas probadas, evidencias esperadas y errores frecuentes. El `index` debe incluir el link de la documentación publicada o ejecutable.

Cada anexo individual debe contener:

- Nombre del integrante.
- Rol o responsabilidad.
- Rama de trabajo, commits, merges o PR de código.
- Rama de trabajo, commits, merges o PR de documentación.
- Evidencia breve de la parte que demostrará en vivo.
- Evidencia de que su aporte quedó integrado en la rama común del equipo.

### 3.2 Secuencia sugerida de presentación

1. Presentar nombre del proyecto, equipo y repositorio GitHub.
2. Explicar la arquitectura U1 usando el diagrama del producto.
3. Mostrar Config Server, Eureka, Gateway y microservicios integrados.
4. Ejecutar la demo técnica por Gateway.
5. Mostrar participación de cada integrante en GitHub.
6. Cada integrante muestra la parte que trabajó.
7. Cerrar con hallazgos, problemas y decisiones técnicas.

### 3.3 Criterios mínimos de aceptación

- PDF grupal generado desde la documentación y subido a BL con nombre correcto.
- Presentación del proyecto U1 subida a BL.
- Documentación en MkDocs o herramienta equivalente con guías reproducibles de S01 a S05.
- Evidencia del avance U1 del proyecto final integrado.
- Productos de sesión de todos los integrantes integrados en el avance U1.
- Rama común del equipo con aportes integrados y ejecutables.
- Evidencia de merge, integración o resolución de conflictos cuando aplique.
- La documentación incluye anexos de participación individual, uno por integrante.
- GitHub evidencia aporte individual de cada integrante mediante ramas, commits, merges o PR de código y documentación.
- Cada integrante demuestra en vivo la parte que trabajó.
- Pruebas por consola.
- Diagnóstico técnico.

## 4. Retroalimentacion posterior

Tiempo: 4h fuera del aula.

### 4.1 Mejoras y recomendaciones para la siguiente unidad

Después de la evaluación, cada estudiante debe implementar las mejoras y recomendaciones recibidas. Esta actividad no forma parte de la calificación de la evaluación U1; sirve como preparación para la siguiente unidad.

Trabajo autónomo:

1. Corregir observaciones detectadas en la exposición.
2. Completar o ajustar la documentación.
3. Mejorar evidencias individuales incompletas.
4. Registrar en GitHub los cambios posteriores a la evaluación.
5. Preparar una breve reflexión técnica sobre la mejora aplicada.

## 5. Rúbrica de evaluación

La rúbrica evalúa el entregable y la sustentación del producto U1 presentados durante la sesión.

| Dimensión | Peso | 3 - Logro destacado | 2 - Logro | 1 - Proceso | 0 - Inicio | Puntuación obtenida |
|---|---:|---|---|---|---|---:|
| 1. Integración del producto U1 | 2 | Integra los productos de S01-S05 y los aportes de todos los integrantes en un sistema base funcionando como un todo. | Integra los componentes principales del producto U1. | La integración de componentes o aportes es parcial. | No evidencia integración. | |
| 2. Funcionamiento técnico U1 | 2 | Demuestra configuración externa, registro y descubrimiento, acceso por Gateway, CRUD persistente y distribución entre múltiples instancias. | Demuestra el funcionamiento de los componentes principales de U1. | El funcionamiento es parcial o presenta fallos relevantes. | No demuestra el funcionamiento del producto U1. | |
| 3. Pruebas, evidencia y diagnóstico | 2 | Ejecuta pruebas reproducibles, presenta resultados verificables y diagnostica con claridad fallos de configuración, descubrimiento, rutas o persistencia. | Presenta pruebas y evidencia suficientes, y explica la causa probable de un fallo. | Las pruebas, evidencias o el diagnóstico son incompletos. | No presenta evidencia verificable ni diagnostica. | |
| 4. Aporte individual, GitHub y demo | 2 | El aporte individual de código y documentación es verificable en GitHub y anexos, está integrado en la rama común y se demuestra en vivo con autonomía. | El aporte es identificable, está integrado y se demuestra adecuadamente. | El aporte es poco trazable, no esta claramente integrado o la demo es parcial. | No se identifica ni demuestra el aporte individual. | |
| 5. Defensa técnica | 1 | Explica decisiones y responde las preguntas con precisión, autonomía y criterio técnico. | Explica las decisiones principales y responde adecuadamente. | Responde parcialmente o con escaso sustento técnico. | No sustenta su trabajo. | |
| 6. Presentación, documentación y reproducibilidad | 1 | Presentación clara; sitio y PDF ordenados por S01-S05, con guías reproducibles, enlace en el index y anexos individuales completos. | La presentación y la documentación permiten comprender y reproducir el flujo principal. | La presentación es poco clara o la documentación es incompleta y poco reproducible. | No presenta documentación o presentación suficiente. | |

Puntuación acumulada = suma de (`Peso` * `Puntuacion obtenida`) = ____.

Nota final = (`Puntuacion acumulada` / 30) * 20 = ____.

Para usar la rúbrica con IA, solicita:

```text
Evalúa el PDF, la presentación, la documentación, la participación en GitHub y la demo individual usando la rúbrica de la sesión.
Para cada dimensión selecciona la puntuación obtenida usando la escala Inicio=0, Proceso=1, Logro=2, Logro destacado=3.
Justifica brevemente cada puntuación.
Calcula la puntuación acumulada con la fórmula: suma de (Peso * Puntuación obtenida).
Calcula la nota final sobre 20 con la fórmula: (Puntuación acumulada / 30) * 20.
Indica 2 fortalezas y 2 recomendaciones.
```
