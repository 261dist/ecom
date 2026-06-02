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

Revisar que la documentacion explique como levantar e integrar:

- `infra`.
- `services`.
- `kafka`.
- `obs`.
- `clients/ecom-ng`.

### 2.3 Observabilidad y diagnostico

La revision debe incluir al menos un caso de fallo documentado y su ruta de diagnostico.

## 3. Aplica: actividad practica guiada

Tiempo: 3h.

### 3.1 Revisar README principal y por modulo

Verificar que los comandos funcionen en DEV y PROD local cuando aplique.

### 3.2 Revisar variables y perfiles

Confirmar `.env.example`, perfiles `dev/prod`, puertos, health y rutas.

### 3.3 Ejecutar prueba principal

Repetir el flujo end-to-end principal y registrar incidencias.

### 3.4 Corregir fallos prioritarios

Priorizar fallos que bloquean ejecucion, evidencia o defensa.

### 3.5 Preparar guion de defensa

Asignar a cada integrante:

- Componente.
- Evidencia.
- Pregunta probable.
- Riesgo tecnico.

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
