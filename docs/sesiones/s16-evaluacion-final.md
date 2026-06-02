# S16 - Evaluacion final

## 1. Introduccion

Tiempo: 20 min.

### 1.1 Proposito

Brindar una instancia final para que estudiantes con competencias pendientes demuestren logro tecnico de forma individual.

### 1.2 Resultado de aprendizaje

El estudiante demuestra que puede implementar, ejecutar, diagnosticar o defender una parte critica del sistema sin depender del grupo.

### 1.3 Producto de sesion

Evidencia individual de logro de competencias pendientes.

### 1.4 Motivacion de la sesion

La competencia profesional se demuestra cuando el estudiante puede operar, explicar y defender una parte del sistema bajo condiciones controladas.

### 1.5 Ubicacion en el curso

- Unidad: U3 - Validacion y consolidacion del producto del curso.
- Producto de unidad: producto final del curso validado, documentado, estabilizado y defendido.
- Avance del producto en esta sesion: demostracion individual de competencias pendientes.

## 2. Explica

Tiempo: 15 min.

### 2.1 Conceptos clave

- Competencia pendiente.
- Consigna individual.
- Evidencia verificable.
- Diagnostico tecnico.
- Sustentacion individual.

### 2.2 Arquitectura del producto en `ecom`

La consigna puede tomar cualquier componente del producto:

- `infra`.
- `services`.
- `kafka`.
- `obs`.
- `clients/ecom-ng`.
- `docs`.

### 2.3 Observabilidad y diagnostico

La evaluacion puede incluir diagnosticar una falla provocada por el docente y explicar la ruta de revision.

## 3. Aplica: actividad practica guiada

Tiempo: 3h.

### 3.1 Identificar competencia pendiente

El docente define la competencia que el estudiante debe demostrar.

### 3.2 Asignar consigna individual

Ejemplos:

- Probar un endpoint.
- Corregir una ruta.
- Diagnosticar un 503.
- Obtener token y consumir una ruta protegida.
- Verificar un evento.
- Consultar BD.
- Explicar un componente.

### 3.3 Ejecutar y evidenciar

El estudiante ejecuta comandos, muestra resultados y explica lo realizado.

### 3.4 Sustentar resultado

El estudiante responde preguntas sobre su procedimiento, errores y decisiones.

## 4. Crea: actividad autonoma

Tiempo: 4h fuera del aula.

### 4.1 Plantilla de evidencia individual

Entrega un PDF:

```text
S16_Equipo##_ApellidoNombre.pdf
```

#### 4.1.1 Datos del estudiante

- Nombre:
- Equipo:
- Sesion: S16 - Evaluacion final
- Rol o aporte realizado:
- Link de GitHub:

#### 4.1.2 Trabajo autonomo realizado

1. Registrar competencia demostrada.
2. Documentar consigna asignada.
3. Mostrar comandos o evidencias.
4. Explicar diagnostico o resultado.
5. Registrar mejora o aprendizaje.

### 4.2 Criterios minimos de aceptacion

- PDF con nombre correcto.
- Competencia identificada.
- Consigna ejecutada.
- Evidencia verificable.
- Sustentacion individual.

## 5. Cierre evaluativo

Tiempo: 20 min.

### 5.1 Resultados esperados

- Competencia pendiente demostrada.
- Evidencia individual presentada.
- Resultado registrado.
- Retroalimentacion final aplicada.

### 5.2 Evidencia del producto de sesion

Entrega individual:

```text
S16_Equipo##_ApellidoNombre.pdf
```

### 5.3 Preguntas de defensa y reflexion

1. Que competencia estas demostrando?
2. Que comando ejecutaste y por que?
3. Que evidencia confirma el resultado?
4. Como corregirias el fallo presentado?
5. Que aprendiste respecto a tu aporte en el sistema?

### 5.4 Rubrica de evaluacion

| Dimension | Peso | 3 - Logro destacado | 2 - Logro | 1 - Proceso | 0 - Inicio | Puntuacion obtenida |
|---|---:|---|---|---|---|---:|
| 1. Ejecucion tecnica | 2 | Ejecuta la consigna correctamente y explica cada paso. | Ejecuta la consigna principal. | Ejecucion parcial. | No ejecuta la consigna. | |
| 2. Diagnostico | 2 | Diagnostica sintomas, causa y solucion. | Explica causa probable. | Diagnostico parcial. | No diagnostica. | |
| 3. Evidencia verificable | 2 | Presenta evidencia clara, reproducible y suficiente. | Evidencia suficiente. | Evidencia incompleta. | No presenta evidencia. | |
| 4. Sustentacion individual | 2 | Responde con autonomia y criterio tecnico. | Responde adecuadamente. | Responde parcialmente. | No sustenta. | |
| 5. Correccion o mejora | 1 | Corrige o propone mejora pertinente. | Propone mejora general. | Mejora poco clara. | No propone mejora. | |
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
