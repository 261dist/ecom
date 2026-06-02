# S14 - Revision tecnica y estabilizacion del producto

## 1. Introduccion

Tiempo: 20 min.

### 1.1 Proposito

Cerrar brechas tecnicas, ordenar documentacion y asegurar que el producto sea reproducible por el docente.

### 1.2 Resultado de aprendizaje

El estudiante estabiliza el producto, corrige fallos, documenta ejecucion y prepara defensa tecnica.

### 1.3 Producto de sesion

Producto documentado, reproducible, depurado y con evidencias organizadas para defensa.

### 1.4 Motivacion de la sesion

Un producto final no solo debe funcionar en la maquina del equipo. Debe poder levantarse, probarse, diagnosticarse y explicarse con documentos claros.

### 1.5 Ubicacion en el curso

- Unidad: U3 - Validacion y consolidacion del producto del curso.
- Producto de unidad: producto final del curso validado, documentado, estabilizado y defendido.
- Avance del producto en esta sesion: estabilizacion final antes de defensa.

## 2. Explica

Tiempo: 15 min.

### 2.1 Conceptos clave

- Reproducibilidad.
- Documentacion tecnica.
- Checklist operativo.
- Incidencias.
- Guion de defensa.

### 2.2 Arquitectura del producto en `ecom`

Revisar que la documentacion explique como levantar e integrar el producto completo.

#### 2.2.1 Revision tecnica en DEV

```mermaid
flowchart TB
    Doc["Documentacion<br/>README + docs"]
    Cliente["Cliente<br/>PowerShell / bash / ecom-ng"]
    Infra["infra<br/>Config + Eureka + Gateway"]
    Services["services<br/>microservicios"]
    Kafka["kafka<br/>broker + UI"]
    Obs["obs<br/>Prometheus + Loki + Grafana"]
    Evidencias["Evidencias<br/>PDF + capturas + comandos"]

    Doc --> Cliente
    Cliente --> Infra
    Infra --> Services
    Services --> Kafka
    Services -.-> Obs
    Cliente --> Evidencias
    Infra --> Evidencias
    Services --> Evidencias
    Kafka --> Evidencias
    Obs --> Evidencias
```

#### 2.2.2 Revision tecnica en PROD local

```mermaid
flowchart TB
    Doc["Documentacion<br/>README + .env.example"]

    subgraph Docker["Docker local"]
        Infra["infra<br/>Config + Eureka + Gateway"]
        Services["services<br/>microservicios + DB"]
        Kafka["kafka<br/>broker + UI"]
        Obs["obs<br/>Prometheus + Loki + Grafana"]
    end

    Cliente["Cliente<br/>PowerShell / bash / navegador"]
    Evidencias["Evidencias finales<br/>comandos + capturas + diagnostico"]

    Doc --> Infra
    Doc --> Services
    Doc --> Kafka
    Doc --> Obs
    Cliente --> Infra
    Infra --> Services
    Services --> Kafka
    Services -.-> Obs
    Cliente --> Evidencias
    Docker --> Evidencias
```

### 2.3 Observabilidad y diagnostico

La revision debe incluir al menos un caso de fallo documentado y su ruta de diagnostico.

## 3. Aplica: actividad practica guiada

Tiempo: 3h.

En el laboratorio, el docente guia una revision tecnica final. El equipo no solo demuestra que funciona: deja el producto ordenado, reproducible y defendible.

### 3.1 Preparar checklist de estabilizacion

Producto del paso: lista de verificacion acordada por equipo.

Checklist minimo:

- README principal.
- README por modulo.
- `.env.example`.
- Comandos DEV.
- Comandos PROD local.
- Health por componente.
- Flujo end-to-end.
- Evidencias por integrante.

### 3.2 Revisar README principal y por modulo

Verificar que los comandos funcionen en DEV y PROD local cuando aplique.

Producto del paso: documentacion alineada al codigo real.

### 3.3 Revisar variables y perfiles

Confirmar `.env.example`, perfiles `dev/prod`, puertos, health y rutas.

Producto del paso: configuracion externa comprensible y sin secretos innecesarios.

### 3.4 Validar comandos DEV

Producto del paso: el sistema se puede levantar desde consola en desarrollo.

Probar, como minimo:

- Config Server.
- Eureka.
- Gateway.
- Dos microservicios.
- Kafka u observabilidad si participan en el flujo.

### 3.5 Validar comandos PROD local

Producto del paso: el sistema se puede levantar con Docker Compose.

Probar:

```bash
cd infra
docker compose up -d --build
```

Luego levantar los modulos necesarios y verificar health.

### 3.6 Ejecutar prueba principal

Repetir el flujo end-to-end principal y registrar incidencias.

Producto del paso: flujo funcional y reproducible.

### 3.7 Registrar incidencias tecnicas

Producto del paso: errores descritos con causa probable y decision tomada.

Usar formato:

```text
Incidencia:
Causa probable:
Evidencia:
Accion aplicada:
Resultado:
```

### 3.8 Corregir fallos prioritarios

Priorizar fallos que bloquean ejecucion, evidencia o defensa.

Producto del paso: producto estabilizado para la defensa.

### 3.9 Revisar observabilidad minima

Producto del paso: diagnostico basico disponible.

Verificar:

- Health de Gateway.
- Logs de un microservicio.
- Una metrica o panel.
- Un correlation id si aplica.

### 3.10 Revisar seguridad

Producto del paso: rutas protegidas y publicas verificadas.

Probar:

- Login correcto.
- Ruta protegida con token.
- Ruta protegida sin token.

### 3.11 Revisar mensajeria y consistencia

Producto del paso: topics, eventos y estados finales coherentes.

Verificar:

- `orden-eventos`.
- `pago-eventos`.
- Estado final de orden.
- Registro de pago.

### 3.12 Preparar guion de defensa

Asignar a cada integrante:

- Componente.
- Evidencia.
- Pregunta probable.
- Riesgo tecnico.

### 3.13 Preparar evidencias individuales

Producto del paso: cada estudiante tiene evidencia propia.

Cada integrante debe tener:

- Captura o comando de su aporte.
- Explicacion breve.
- Link de GitHub.
- Riesgo o aprendizaje tecnico.

### 3.14 Validar repositorio GitHub

Producto del paso: trabajo versionado y revisable.

Verificar:

- Rama o tag usado.
- Commits del equipo.
- README actualizado.
- Archivos generados no necesarios fuera del repo.

### 3.15 Ejecutar simulacro breve de defensa

Producto del paso: cada integrante responde al menos una pregunta tecnica.

El docente puede seleccionar integrantes al azar y pedir evidencia directa.

### 3.16 Cerrar pendientes

Producto del paso: lista corta de pendientes o confirmacion de cierre.

Clasificar:

- Bloqueante.
- Importante pero no bloqueante.
- Mejora futura.

### 3.17 Ruta alternativa: clonar y ejecutar a partir del tag final de la sesion

```bash
git clone --branch vs14-estabilizacion-final https://github.com/261dist/ecom.git ecom-s14
cd ecom-s14
```

## 4. Crea: actividad autonoma

Tiempo: 4h fuera del aula.

### 4.1 Plantilla de evidencia individual

Entrega un PDF:

```text
S14_Equipo##_ApellidoNombre.pdf
```

#### 4.1.1 Datos del estudiante

- Nombre:
- Equipo:
- Sesion: S14 - Revision tecnica y estabilizacion del producto
- Rol o aporte realizado:
- Link de GitHub:

#### 4.1.2 Trabajo autonomo realizado

1. Corregir una incidencia o mejorar documentacion.
2. Validar comandos reales.
3. Preparar evidencia final.
4. Ensayar defensa individual.
5. Registrar riesgo tecnico pendiente, si existe.

### 4.2 Criterios minimos de aceptacion

- PDF con nombre correcto.
- Evidencia de estabilizacion o documentacion.
- Comandos validados.
- Aporte individual verificable.
- Defensa preparada.

## 5. Cierre evaluativo

Tiempo: 20 min.

### 5.1 Resultados esperados

- README y evidencias ordenadas.
- Producto reproducible.
- Incidencias prioritarias cerradas.
- Defensa preparada por integrante.

### 5.2 Evidencia del producto de sesion

Entrega individual:

```text
S14_Equipo##_ApellidoNombre.pdf
```

### 5.3 Preguntas de defensa y reflexion

1. Que cambio tecnico estabilizaste?
2. Como sabe el docente que el proyecto es reproducible?
3. Que evidencia individual presentaras?
4. Que riesgo tecnico queda y como lo mitigarias?

### 5.4 Rubrica de evaluacion

| Dimension | Peso | 3 - Logro destacado | 2 - Logro | 1 - Proceso | 0 - Inicio | Puntuacion obtenida |
|---|---:|---|---|---|---|---:|
| 1. Reproducibilidad | 2 | Comandos probados y documentados claramente. | Comandos principales validados. | Validacion parcial. | No evidencia reproducibilidad. | |
| 2. Documentacion | 2 | README completo y alineado al codigo. | README suficiente. | Documentacion incompleta. | No evidencia documentacion. | |
| 3. Correccion de incidencias | 2 | Incidencias cerradas con evidencia. | Incidencias principales atendidas. | Correccion parcial. | No corrige incidencias. | |
| 4. Preparacion de defensa | 2 | Guion y evidencias por integrante claros. | Defensa preparada. | Preparacion parcial. | No evidencia preparacion. | |
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
