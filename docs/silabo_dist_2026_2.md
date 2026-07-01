<!-- Version 2026-2 construida desde silabo_dist_2026_1.md y docs/index.md -->

Universidad Peruana Union  
Carret. Central km. 19.5 Nana. Telf. 01-6186300 Casilla 3564 Lima 1, Peru

# Silabo: Desarrollo de Aplicaciones Distribuidas

## I. Informacion General de Asignatura

| N. | Campo | Informacion | N. | Campo | Informacion |
|---|---|---|---|---|---|
| 01 | Facultad/EGP | Facultad de Ingenieria y Arquitectura | 09 | Ano de plan de estudio | 2024-1 |
| 02 | Programa de estudio | EP Ingenieria de Sistemas | 10 | Ciclo de estudio | 5 |
| 03 | Tipo de estudio | Especialidad | 11 | Codigo de asignatura |  |
| 04 | Nombre de asignatura | Desarrollo de Aplicaciones Distribuidas | 12 | Numero de creditos | 3 |
| 05 | Duracion |  | 13 | Nota minima probatoria | 13 |
| 06 | Horas de la asignatura | H. Te. Pract: 2 / H. Prc. Pres: 2 | 14 | Ano y semestre academico | 2026-2 |
| 07 | Docente | Sullon Macalupu Abel Angel |  |  |  |
| 08 | Pre requisito | Lenguaje de Programacion II |  |  |  |

## II. Sumilla

La asignatura es de naturaleza teorico-practica, pertenece al Area de Estudios Especificos y Especialidad y a la subarea de Ingenieria de Software. Su proposito es brindar al estudiante los conocimientos necesarios para desarrollar aplicaciones distribuidas mediante microservicios, configuracion centralizada, descubrimiento de servicios, API Gateway, seguridad, resiliencia, mensajeria asincrona, consistencia distribuida, observabilidad e integracion frontend. El curso desarrolla progresivamente un sistema distribuido de comercio electronico ejecutable en entornos reproducibles con Docker y Spring Cloud.

## III. Competencia del perfil de egreso en relacion a la asignatura

| Tipo | Competencia | Nivel / dimensiones |
|---|---|---|
| Especifica | **INGENIERIA DE SOFTWARE:** Gestiona y desarrolla software de manera eficiente y efectiva, basandose en estandares internacionales de calidad a fin de lograr el control y aseguramiento de la calidad segun el contexto de la organizacion. | N. 1.1: Programacion. Desarrolla aplicaciones de escritorio, web y movil. |
| General | **CARACTER Y APRENDIZAJE AUTONOMO:** Cultiva un caracter integro y autonomo, guiado por principios biblicos y adventistas, integrando un enfoque espiritual con la proactividad en el aprendizaje y el desarrollo personal. | N. 1.1: Firmeza de Proposito, Ejecucion, Dominio Propio, Mantener el Esfuerzo, Salud SocioEmocional. |

## IV. Resultado de aprendizaje de la asignatura

| Resultado de aprendizaje | Producto Academico |
|---|---|
| Implementa, integra y sustenta un sistema distribuido basado en microservicios, aplicando configuracion centralizada, descubrimiento de servicios, enrutamiento, escalado, seguridad, comunicacion entre servicios, mensajeria asincrona, consistencia distribuida, observabilidad, persistencia e integracion frontend, validando su funcionamiento mediante evidencias tecnicas y defensa individual de aportes. | **Nombre:** Sistema distribuido de microservicios end-to-end, configurable, escalable, seguro, resiliente, consistente, observable, integrado con frontend y defendido tecnicamente. |
|  | **Descripcion:** Desarrolla un sistema distribuido de comercio electronico mediante laboratorios reproducibles. La solucion integra infraestructura, microservicios, cliente frontend, mensajeria, observabilidad y documentacion tecnica. El producto se presenta en equipo, pero cada estudiante evidencia y defiende su aporte individual. |

## V. Unidades de aprendizaje

## Unidad 1: Sistema distribuido base orientado a produccion

| Resultado de aprendizaje | Producto |
|---|---|
| Construye un primer servicio REST funcional, externaliza configuracion por ambientes, registra servicios dinamicamente, accede al sistema mediante un punto unico de entrada y demuestra distribucion de trafico entre instancias. | **Nombre:** Sistema distribuido base funcional, configurable y preparado para multiples instancias. |

| Criterios de evaluacion del producto | Descripcion del producto |
|---|---|
| Servicio REST funcional y persistente. Configuracion externa por ambiente. Registro y descubrimiento de servicios operativo. Punto unico de acceso mediante Gateway. Distribucion de trafico entre instancias. Evidencias de ejecucion reproducible y documentacion tecnica basica. | Implementa la base tecnica del sistema distribuido: un servicio REST funcional, configuracion centralizada, descubrimiento dinamico, acceso por Gateway y ejecucion concurrente de instancias. |

### Sesiones de aprendizaje

| N. | Fecha | Contenido | HT | HP | Actividad practica | Actividad autonoma |
|---|---|---|---|---|---|---|
| 1 | 19-03-2026 | Construccion de un servicio base para un sistema distribuido. | 2 | 2 | Implementa un servicio REST funcional, persistente, observable y preparado para ejecucion reproducible. | Replica el patron del servicio base en otro recurso del proyecto y documenta endpoints principales. |
| 2 | 26-03-2026 | Gestion centralizada de configuracion y ambientes. | 2 | 2 | Externaliza configuracion por ambiente e incorpora evidencia inicial de observabilidad. | Configura variables y perfiles para otro microservicio del proyecto integrador. |
| 3 | 02-04-2026 | Registro, descubrimiento y ejecucion concurrente de servicios. | 2 | 2 | Registra servicios dinamicamente y ejecuta multiples instancias operativas. | Valida el descubrimiento de servicios y documenta evidencias de instancias activas. |
| 4 | 09-04-2026 | Punto unico de acceso y distribucion de trafico. | 2 | 2 | Configura rutas de acceso centralizado con Gateway y balanceo de carga. | Integra nuevas rutas del proyecto mediante Gateway y registra pruebas de acceso. |
| 5 | 16-04-2026 | Evaluacion U1: Sistema distribuido base. | 2 | 2 | Sustenta el sistema base integrado funcionando como un todo. | Corrige observaciones, estabiliza configuracion y actualiza documentacion tecnica de U1. |

## Unidad 2: Sistema distribuido robusto

| Resultado de aprendizaje | Producto |
|---|---|
| Implementa comunicacion sincronica resiliente, seguridad distribuida, mensajeria asincrona, consistencia eventual en procesos de negocio, observabilidad operacional e integracion frontend mediante el punto unico de acceso. | **Nombre:** Sistema distribuido seguro, resiliente, consistente, observable e integrado con cliente frontend. |

| Criterios de evaluacion del producto | Descripcion del producto |
|---|---|
| Comunicacion entre servicios con respuesta controlada ante fallos. Seguridad distribuida y proteccion de rutas. Mensajeria asincrona entre servicios desacoplados. Consistencia eventual, compensacion e idempotencia en procesos de negocio. Logs, health, metricas y paneles de diagnostico. Cliente frontend integrado mediante Gateway. | Fortalece el sistema distribuido incorporando atributos de calidad, integracion frontend y evidencias tecnicas de operacion real. |

### Sesiones de aprendizaje

| N. | Fecha | Contenido | HT | HP | Actividad practica | Actividad autonoma |
|---|---|---|---|---|---|---|
| 6 | 23-04-2026 | Comunicacion sincronica resiliente entre servicios. | 2 | 2 | Implementa comunicacion entre microservicios con respuesta controlada ante fallos. | Agrega escenarios de fallo, fallback y recuperacion al flujo principal del proyecto. |
| 7 | 30-04-2026 | Seguridad distribuida y control de acceso. | 2 | 2 | Implementa autenticacion, autorizacion y proteccion de rutas del sistema. | Protege endpoints del proyecto, documenta roles y valida accesos permitidos y denegados. |
| 8 | 07-05-2026 | Mensajeria asincrona entre servicios. | 2 | 2 | Implementa comunicacion por eventos entre servicios desacoplados. | Integra un evento de negocio adicional y registra evidencias de publicacion y consumo. |
| 9 | 14-05-2026 | Consistencia distribuida en procesos de negocio. | 2 | 2 | Implementa un proceso distribuido con consistencia eventual, compensacion e idempotencia. | Documenta el flujo de negocio, estados, compensaciones y pruebas de idempotencia. |
| 10 | 21-05-2026 | Observabilidad y diagnostico de sistemas distribuidos. | 2 | 2 | Incorpora logs, health, metricas y paneles de diagnostico. | Registra evidencias de monitoreo, diagnostico de fallos y trazabilidad operacional. |
| 11 | 28-05-2026 | Integracion con cliente frontend. | 2 | 2 | Integra el cliente web al sistema distribuido mediante Gateway. | Completa flujos frontend-backend con seguridad y consumo de APIs protegidas. |
| 12 | 04-06-2026 | Evaluacion U2: Sistema distribuido robusto. | 2 | 2 | Sustenta el sistema robusto validado en condiciones reales. | Corrige observaciones, consolida evidencias y prepara la validacion end-to-end de U3. |

## Unidad 3: Validacion y consolidacion del producto del curso

| Resultado de aprendizaje | Producto |
|---|---|
| Integra los componentes desarrollados en las unidades anteriores, valida flujos completos, estabiliza documentacion y despliegue local, prepara evidencias tecnicas y sustenta el producto final. | **Nombre:** Sistema distribuido de microservicios end-to-end, validado, documentado, estabilizado y defendido tecnicamente. |

| Criterios de evaluacion del producto | Descripcion del producto |
|---|---|
| Producto probado integralmente. Documentacion tecnica completa y reproducible. Evidencias de despliegue, seguridad, mensajeria, consistencia y observabilidad. Defensa grupal coherente y aporte individual verificable. Correccion de observaciones y demostracion de competencias pendientes. | Consolida el producto final del curso, valida flujos completos, estabiliza la arquitectura y sustenta tecnicamente las decisiones implementadas. |

### Sesiones de aprendizaje

| N. | Fecha | Contenido | HT | HP | Actividad practica | Actividad autonoma |
|---|---|---|---|---|---|---|
| 13 | 11-06-2026 | Validacion end-to-end del producto del curso. | 2 | 2 | Ejecuta pruebas integrales del producto del curso. | Documenta evidencias end-to-end y corrige fallos detectados en flujos principales. |
| 14 | 18-06-2026 | Revision tecnica y estabilizacion del producto. | 2 | 2 | Estabiliza documentacion, evidencias, configuracion y despliegue local. | Refina manual de ejecucion, prepara repositorio final y levanta observaciones tecnicas. |
| 15 | 25-06-2026 | Defensa tecnica. | 2 | 2 | Sustenta grupalmente el producto y defiende decisiones tecnicas de arquitectura. | Consolida aportes individuales, evidencias finales y respuestas a observaciones. |
| 16 | 02-07-2026 | Evaluacion final. | 2 | 2 | Demuestra individualmente competencias pendientes del curso. | Reflexiona sobre aprendizajes, fortalezas, oportunidades de mejora y cierre tecnico del producto. |

## VI. Estrategias metodologicas

| N. | Estrategias de ensenanza y de aprendizaje que se aplicaran en la asignatura |
|---|---|
| 1.1 | Flipped Classroom (Clase Invertida): En esta metodologia, los estudiantes revisan el material teorico fuera del aula, generalmente en linea, y utilizan el tiempo en clase para actividades practicas y discusiones. |
| 1.2 | Aprendizaje Basado en Problemas: Centra el aprendizaje en la resolucion de problemas reales, una habilidad esencial en casi todas las profesiones. Estimula el pensamiento critico y la colaboracion, elementos clave en el desarrollo de competencias. |
| 1.3 | Proyectos: Fomentan habilidades de investigacion, gestion del tiempo y trabajo en equipo, todas cruciales en el mundo profesional. |

## VII. Evaluacion

La evaluacion de los estudiantes se rige por el Reglamento de Estudios, disponible en: <https://upeu.edu.pe/reglamentos/evaluacion/>.

La estructura evaluativa comprende componentes formativos y/o de procesos, de producto y genericos, reflejando un enfoque integral.

### Componentes de evaluacion y ponderacion

- **Evaluacion de Sesiones (ES):** Es el promedio de las evaluaciones aplicadas a los estudiantes para verificar su proceso de aprendizaje durante las sesiones de las unidades. Su contribucion a la nota final es de hasta el 20%.
- **Evaluacion de Productos (EP):** Es el promedio ponderado de las evaluaciones de los productos entregados en cada unidad. Este componente representa un minimo del 70% de la nota final.
- **Evaluacion de Competencias Generales (ECG):** Esta evaluacion aporta hasta un 10% al calculo de la nota final.

### Programacion de evaluaciones

| Fecha | Unidad | Producto | Evaluacion de proceso y de resultado | Pesos |
|---|---|---|---|---|
| 16/04/2026 | Unidad 1: Sistema distribuido base orientado a produccion | Sistema distribuido base funcional, configurable y preparado para multiples instancias. | Evaluacion de sesiones | 5% |
| 16/04/2026 | Unidad 1: Sistema distribuido base orientado a produccion | Sistema distribuido base funcional, configurable y preparado para multiples instancias. | Evaluacion del producto | 15% |
| 04/06/2026 | Unidad 2: Sistema distribuido robusto | Sistema distribuido seguro, resiliente, consistente, observable e integrado con cliente frontend. | Evaluacion de sesiones | 5% |
| 04/06/2026 | Unidad 2: Sistema distribuido robusto | Sistema distribuido seguro, resiliente, consistente, observable e integrado con cliente frontend. | Evaluacion del producto | 30% |
| 02/07/2026 | Unidad 3: Validacion y consolidacion del producto del curso | Sistema distribuido de microservicios end-to-end, validado, documentado, estabilizado y defendido tecnicamente. | Evaluacion de sesiones | 10% |
| 02/07/2026 | Unidad 3: Validacion y consolidacion del producto del curso | Sistema distribuido de microservicios end-to-end, validado, documentado, estabilizado y defendido tecnicamente. | Evaluacion del producto | 25% |
| 02/07/2026 | Competencia General | CARACTER Y APRENDIZAJE AUTONOMO: Cultiva un caracter integro y autonomo, guiado por principios biblicos y adventistas, integrando un enfoque espiritual con la proactividad en el aprendizaje y el desarrollo personal. | Competencia General | 10% |

| Componente | Peso |
|---|---|
| Evaluacion de sesiones | 20% |
| Evaluacion del producto | 70% |
| Evaluacion de competencia generica | 10% |
| **Total** | **100%** |

## VIII. Recursos, medios y materiales

| N. | Recursos, medios y materiales |
|---|---|
| 1 | Guias y/o tutoriales |
| 2 | Laboratorios |
| 3 | Internet - Wifi |
| 4 | Proyector y/o TV Smart |

## IX. Referencias

### Basica (Fuentes primarias)

- Philippe J. 2018. *Docker Primeros pasos y puesta en practica de una arquitectura basada en micro-servicios*. Ediciones ENI.
- Mathur, A. (2021). *Traefik API Gateway for Microservices*. Gurgaon, Haryana, India. ISBN-13 (electronic): 978-1-4842-6376-1. doi: <https://doi.org/10.1007/978-1-4842-6376-1>.
- Singh, N. (2021). *Building Microservices with Micronaut*. ISBN 978-1-80056-423-7.
- Carnell J. 2017. *Spring Microservices in Action*. Shelter Island. Manning Publications Co.
- Lamouchi, N. (2021). *Pro Java Microservices with Quarkus and Kubernetes: A Hands-on Guide*. Paris, France. ISBN-13 (electronic): 978-1-4842-7170-4.
- Patni, S. (2023). *Pro RESTful APIs with Micronaut: Build Java-Based Microservices with*. Santa Clara, CA, USA. ISBN-13 (electronic): 978-1-4842-9200-6.
- Arango E. C., Loaiza O. L. (2021). SCRUM Framework Extended with Clean Architecture Practices for Software Maintainability. In Silhavy R. (eds), *Software Engineering and Algorithms*. CSOC 2021. Lecture Notes in Networks and Systems, vol. 230. Springer, Cham. <https://doi.org/10.1007/978-3-030-77442-4_56>.
- Christudas, B. (2019). *Practical Microservices Architectural Patterns*. Trivandrum, Kerala, India. ISBN-13 (electronic): 978-1-4842-4501-9.
- De La Torre C., Wagner B., Rousos M. 2022. *.NET Microservices: Architecture for Containerized .NET Applications*. Washington. Microsoft Corporation.
- Martinez D., Valderes P., Torres V. 2018. *Microservicios: un enfoque integrado*. Madrid: RA-MA Editorial.
- Berenguel J. 2016. *Desarrollo de aplicaciones web distribuidas UF1824*. Espana: Ediciones Paraninfo S.A.
- Schenker G. 2018. *Containerize your Apps with Docker and Kubernetes*. Packt Publishing Ltd.
- Boada M., Gomez J. 2018. *El Gran libro de Angular*. Mexico: Alfaomega Grupo Editor.
- Palacio R., Moran A. 2015. *Inicios de colaboracion en el desarrollo distribuido de software*.
- Gonzalez M., Perez A. 2021. *Criptografia esencial*. Madrid: RA-MA Editorial.

### Enlaces de internet

- <http://www.ucuenca.edu.ec/ojs/index.php/maskana/article/view/695>
- <http://asiermarques.com/2013/conceptos-sobre-apis-rest/>
- <https://hub.docker.com/>
- <http://tesis.ipn.mx/handle/123456789/19869>
- <https://www.youtube.com/watch?v=OJuNzSwsZaY>
- <https://angular.io/>
- <http://sedici.unlp.edu.ar/handle/10915/56635>
- <https://aws.amazon.com/es/microservices/>
- <https://dialnet.unirioja.es/servlet/articulo?codigo=5123616>
- <https://es.reactjs.org/>
- <https://material.angular.io/>
- <https://www.docker.com/>