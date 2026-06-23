# S15 - Defensa técnica

## 1. Instrucciones iniciales

Tiempo: 5 min.

### 1.1 Propósito

Sustentar técnicamente el producto del curso, las decisiones tomadas, las evidencias obtenidas y el aporte individual de cada integrante.

### 1.2 Resultado de aprendizaje

El estudiante explica, demuestra y defiende su contribucion dentro de un sistema distribuido completo.

### 1.3 Producto de sesión

Defensa técnica grupal del producto del curso con nota individual.

### 1.4 Preguntas del docente durante la sustentación

Defender un sistema distribuido exige demostrar arquitectura, flujos, fallos, diagnóstico, datos y decisiones técnicas. No basta con ejecutar una demo.

Preguntas que el docente puede realizar a cada estudiante:

1. Qué parte del producto desarrollaste y cómo se integra con el sistema?
2. Qué evidencia demuestra que tu aporte funciona?
3. Cómo diagnosticarias un fallo relacionado con tu componente?

### 1.5 Ubicación en el curso

- Unidad: U3 - Validación y consolidación del producto del curso.
- Producto de unidad: producto final del curso validado, documentado, estabilizado y defendido.
- Avance del producto en esta sesión: sustentación grupal del producto con evaluación individual.

## 2. Encuadre de la evaluación

Tiempo: 10 min.

El docente presenta brevemente la arquitectura del producto del curso, recuerda la distribución del tiempo y pasa directamente a las exposiciones.

### 2.1 Arquitectura ecom v2026

La arquitectura de referencia para la defensa del producto U3 es la misma arquitectura integral definida en el `index.md`. El equipo debe presentar los componentes que implementó, sus relaciones y el flujo end-to-end. Si realizó adaptaciones para su proyecto, debe reflejarlas en su propio diagrama y justificar técnicamente cada diferencia.

```mermaid
%%{init: {"flowchart": {"nodeSpacing": 18, "rankSpacing": 28, "curve": "basis"}} }%%
flowchart LR
    subgraph Infra["infra"]
        Config["Config<br/>D 18888<br/>P 28888"]
        Eureka["Eureka<br/>D 18761<br/>P 28761"]
        Gateway["Gateway<br/>D 18080<br/>P 28082"]
    end

    subgraph Runtime["microservicios"]
        subgraph Identity["identidad"]
            Auth["auth-ms<br/>(Keycloak u otro)<br/>dinamico"]
            AuthDB["auth_db<br/>D 15431<br/>P 25431"]
            Auth --> AuthDB
        end

        subgraph Services["services"]
            Catalogo["catalogo-ms<br/>dinamico"]
            CatalogoDB["catálogo_db<br/>D 15432<br/>P 25432"]
            Producto["producto-ms<br/>dinamico"]
            ProductoDB["producto_db<br/>D 15433<br/>P 25433"]
            Orden["orden-ms<br/>dinamico"]
            OrdenDB["orden_db<br/>D 15434<br/>P 25434"]
            Pago["pago-ms<br/>dinamico"]
            PagoDB["pago_db<br/>D 15435<br/>P 25435"]

            Catalogo --> CatalogoDB
            Producto --> ProductoDB
            Orden --> OrdenDB
            Pago --> PagoDB
            Producto -->|"consulta categoría"| Catalogo
        end
    end

    subgraph Messaging["kafka"]
        Broker["Kafka broker<br/>D 41092<br/>P 29092"]
        KafkaUI["Kafka UI<br/>D 41085<br/>P 28085"]
        KafkaUI --> Broker
    end

    subgraph External["sistema externo"]
        PaymentGateway["Pasarela<br/>pagos externa"]
    end

    Angular --> Gateway
    Gateway --> Auth
    Gateway --> Catalogo
    Gateway --> Producto
    Gateway --> Orden
    Gateway --> Pago

    Config -. "carga configuración" .-> Eureka
    Config -. "carga configuración" .-> Gateway
    Config -. "carga configuración<br/>configserver" .-> Runtime
    Runtime -. "registra instancias" .-> Eureka
    Gateway -. "descubre servicios" .-> Eureka

    Orden -->|"orden-eventos"| Broker
    Broker -->|"orden-eventos"| Pago
    Pago -->|"pago-eventos"| Broker
    Pago -->|"autoriza / confirma pago"| PaymentGateway

    classDef external fill:#fff3cd,stroke:#b7791f,stroke-width:2px,color:#5f370e;
    class PaymentGateway external;

    subgraph Client["clients"]
        Angular["ecom-ng<br/>D 4200"]
    end

    subgraph Obs["observabilidad"]
        Prometheus["Prometheus<br/>D 19090<br/>P 29090"]
        Loki["Loki<br/>D 13100<br/>P 23100"]
        Grafana["Grafana<br/>D 13000<br/>P 23000"]
        Grafana --> Prometheus
        Grafana --> Loki
    end

    Angular ~~~ Prometheus
```

Las flechas continuas representan interacciones de negocio o consultas directas. Las flechas punteadas representan dependencias de infraestructura, configuración o descubrimiento.

### 2.2 Tiempo de exposición por equipo

Cada equipo dispone de hasta 18 minutos:

- 10 minutos de exposición del producto final.
- 5 minutos de demo técnica.
- 3 minutos de preguntas del docente a los integrantes del equipo.

## 3. Presentación y sustentación del producto

Tiempo: 3h 45 min para la ronda de evaluación de equipos.

En esta sesión se realiza la defensa técnica del producto final. Cada equipo dispone de hasta 18 minutos para presentar su producto, ejecutar la demo y responder preguntas. La rúbrica se aplica al cierre de la exposición de cada equipo.

### 3.1 Plantilla de entrega

La defensa técnica requiere tres entregables grupales:

1. Documentación en MkDocs o una herramienta equivalente, organizada por unidad y sesión, con guías reproducibles.
2. PDF grupal generado como impresion o exportacion directa de la documentación y subido a la plataforma BLearning (BL).
3. Presentación final clara del proyecto (PPT o equivalente) subida a BL.

El PDF debe generarse como impresion o exportacion directa del sitio de documentación. No se acepta un PDF armado manualmente fuera de la documentación del proyecto.

```text
S15_Equipo##_U3_Docs.pdf
```

La presentación final debe entregarse con el nombre:

```text
ProductoCurso_Equipo##_Presentación.pdf
```

La documentación debe estar en el repositorio GitHub y publicarse como sitio navegable, por ejemplo en GitHub Pages (`github.io`) u otra plataforma equivalente. El `index` debe incluir el enlace del sitio publicado.

#### 3.1.1 Datos del equipo

- Equipo:
- Sesión: S15 - Defensa técnica del producto U3
- Proyecto:
- Link de GitHub:
- Link de documentación:
- Rama integrada evaluada:
- Evidencia de integración o merge:
- Integrantes:
- Anexos individuales incluidos:

#### 3.1.2 Evidencia técnica del producto final

- Producto del curso integrado y ejecutable.
- Arquitectura final y flujo end-to-end.
- Seguridad, comunicación síncrona, eventos y consistencia.
- Observabilidad y diagnóstico.
- Frontend integrado mediante Gateway.
- Evidencia de integración de los aportes de todos los integrantes.

#### 3.1.3 Presentación final del proyecto

La presentación debe incluir:

- Nombre del proyecto y equipo.
- Problema o flujo de negocio implementado.
- Arquitectura final del producto.
- Flujo end-to-end.
- Seguridad, eventos, consistencia y observabilidad.
- Integración frontend.
- Evidencias principales.
- Aporte individual de cada integrante.
- Evidencia de participación individual en GitHub.
- Demo asignada a cada integrante.
- Riesgos, incidencias y mejoras futuras.

#### 3.1.4 Documentación en MkDocs o herramienta equivalente

La documentación debe seguir una estructura ordenada por unidad, sesión y anexos. Cada sesión documenta la evolución del proyecto final e integra los aportes realizados por el equipo:

- U1: artefactos de S01 a S05.
- U2: artefactos de S06 a S12.
- U3: validación, estabilización y defensa técnica de S13 a S15.
- Anexos: evidencia de participación individual, un anexo por integrante.

Cada guía debe contener comandos, orden de arranque, puertos, variables de entorno, rutas, datos de prueba, evidencias esperadas, errores frecuentes y criterios de verificación.

Cada anexo individual debe contener:

- Nombre del integrante.
- Rol o responsabilidad.
- Rama de trabajo, commits, merges o pull requests de código.
- Rama de trabajo, commits, merges o pull requests de documentación.
- Evidencia breve de la parte que demostrará en vivo.
- Evidencia de que su aporte quedó integrado en la rama común del equipo.

### 3.2 Secuencia sugerida de presentación

1. Presentar el nombre del proyecto, el equipo y el repositorio GitHub.
2. Explicar el problema o flujo de negocio implementado.
3. Explicar la arquitectura final usando el diagrama del producto.
4. Ejecutar la demo end-to-end.
5. Mostrar seguridad, comunicación, eventos, consistencia y observabilidad.
6. Mostrar la integración frontend y la documentación reproducible.
7. Mostrar la integración y participación de cada integrante en GitHub.
8. Cada integrante demuestra la parte que trabajó.
9. Cerrar con riesgos, incidencias y decisiones técnicas.

### 3.3 Criterios mínimos de aceptación

- PDF grupal generado desde la documentación y subido a BL con el nombre correcto.
- Presentación final clara (PPT o equivalente) subida a BL.
- Documentación publicada como sitio navegable, por ejemplo en GitHub Pages (`github.io`) o equivalente.
- Producto final integrado y ejecutable desde una rama común.
- Arquitectura y flujo end-to-end demostrados.
- Seguridad, eventos, consistencia y observabilidad demostrados.
- Productos de sesión y unidad de todos los integrantes integrados.
- Evidencia de merge, integración o resolución de conflictos cuando corresponda.
- Un anexo de participación individual por integrante.
- GitHub evidencia aportes de código y documentación.
- Cada integrante demuestra en vivo la parte que trabajó.

## 4. Retroalimentacion posterior

Tiempo: 4h fuera del aula.

### 4.1 Mejoras y recomendaciones

Las mejoras indicadas después de la evaluación no forman parte de la calificación de S15. Sirven para fortalecer el portafolio y, cuando corresponda, preparar la demostración individual de competencias pendientes en S16.

1. Corregir las observaciones detectadas durante la defensa.
2. Completar o ajustar la documentación del producto.
3. Mejorar las evidencias individuales incompletas.
4. Registrar en GitHub los cambios posteriores a la evaluación.
5. Preparar la competencia pendiente que deba demostrarse en S16.

## 5. Rúbrica de evaluación

La rúbrica evalúa el entregable grupal, la sustentación del producto y la demostración individual realizada durante S15. Se aplica al cierre de los 18 minutos asignados a cada equipo.

| Dimensión | Peso | 3 - Logro destacado | 2 - Logro | 1 - Proceso | 0 - Inicio | Puntuación obtenida |
|---|---:|---|---|---|---|---:|
| 1. Integración del producto U3 | 2 | Integra los productos de U1, U2 y U3 y los aportes de todos los integrantes en el producto final funcionando end-to-end. | Integra los componentes principales del producto final. | La integración de unidades, componentes o aportes es parcial. | No evidencia integración del producto final. | |
| 2. Funcionamiento técnico U3 | 2 | Demuestra el flujo end-to-end con infraestructura, servicios, seguridad, eventos, consistencia, observabilidad, frontend y sistema externo. | Demuestra el funcionamiento de los componentes principales del producto final. | El funcionamiento es parcial o presenta fallos relevantes. | No demuestra el funcionamiento del producto final. | |
| 3. Pruebas, evidencia y diagnóstico | 2 | Ejecuta una demo reproducible, presenta evidencia integral y diagnostica fallos mediante datos, logs, métricas, eventos o trazas. | Presenta pruebas y evidencia suficientes, y explica la causa probable de un fallo. | Las pruebas, evidencias o el diagnóstico son incompletos. | No presenta evidencia verificable ni diagnostica. | |
| 4. Aporte individual, GitHub y demo | 2 | El aporte individual de código y documentación es verificable en GitHub y anexos, está integrado en la rama común y se demuestra en vivo con autonomía. | El aporte es identificable, está integrado y se demuestra adecuadamente. | El aporte es poco trazable, no esta claramente integrado o la demo es parcial. | No se identifica ni demuestra el aporte individual. | |
| 5. Defensa técnica | 1 | Explica la arquitectura y las decisiones, y responde con precisión, autonomía y criterio técnico. | Explica las decisiones principales y responde adecuadamente. | Responde parcialmente o con escaso sustento técnico. | No sustenta su trabajo. | |
| 6. Presentación, documentación y reproducibilidad | 1 | Presentación final clara; sitio y PDF ordenados por unidad y sesión, con guías reproducibles, enlace en el index y anexos individuales completos. | La presentación y la documentación permiten comprender y reproducir el flujo end-to-end. | La presentación es poco clara o la documentación es incompleta y poco reproducible. | No presenta documentación o presentación suficiente. | |

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
