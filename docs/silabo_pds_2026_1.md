<!-- Transcripción fiel generada desde: PDS.docx -->

Universidad Peruana Unión  
Carret. Central km. 19.5 Ñaña. Telf. 01-6186300 Casilla 3564 Lima 1, Perú

# Sílabo: Pruebas y Despliegue del Software

## I. Información General de Asignatura

| N. | Campo | Información | N. | Campo | Información |
|---|---|---|---|---|---|
| 01 | Facultad/EGP | Facultad de Ingeniería y Arquitectura | 09 | Año de plan de estudio | 2023-1 |
| 02 | Programa de estudio | EP Ingeniería de Sistemas | 10 | Ciclo de estudio | 7 |
| 03 | Tipo de estudio | General | 11 | Código de asignatura |  |
| 04 | Nombre de asignatura | Pruebas y Despliegue del Software | 12 | Número de créditos | 3 |
| 05 | Duración |  | 13 | Nota mínima probatoria | 13 |
| 06 | Horas de la asignatura | H. Te. Pract: 0 / H. Prc. Pres: 32 | 14 | Año y semestre académico | 2026-1 |
| 07 | Docente | Mamani Pari David |  |  |  |
| 08 | Pre requisito | Lenguaje de Programación II |  |  |  |

## II. Sumilla

La asignatura es de carácter teórico práctico, perteneciente al área de formación especializada y sub área de ingeniería de software, cuyo propósito es que el estudiante pueda gestionar el proceso de prueba del software, así como evaluar profesionalmente la calidad del software a través de indicadores. Comprende: Flujo de trabajo de las pruebas de software, diseño de pruebas, planificación y ejecución de las pruebas de software, técnicas y estrategias para la validación y la verificación de productos software y tipos de pruebas.

## III. Competencia del Perfil de Egreso en Relación a la Asignatura

| Tipo | Competencia | Dimensiones |
|---|---|---|
| Específica | **INGENIERÍA DE SOFTWARE:** Gestiona y desarrolla software de manera eficiente y efectiva, basándose en estándares internacionales de calidad a fin de lograr el control y aseguramiento de la calidad según el contexto de la organización. | N. 1.1: Programación, calidad de software. |
| General | **CARÁCTER Y APRENDIZAJE AUTÓNOMO:** Cultiva un carácter íntegro y autónomo, guiado por principios bíblicos y adventistas, integrando un enfoque espiritual con la proactividad en el aprendizaje y el desarrollo personal. | N. 1.1: Firmeza de propósito, ejecución, mantener el esfuerzo. |

## IV. Resultado de Aprendizaje de la Asignatura

| Resultado de aprendizaje | Producto académico |
|---|---|
| Implementa una estrategia completa de pruebas y despliegue aplicando técnicas manuales y automatizadas, integrando pipelines CI/CD para garantizar la calidad y entrega continua de software en un entorno de producción simulado. | **Nombre:** Pipeline CI/CD con suite de pruebas automatizadas. |
|  | **Descripción:** Informe sobre implementación de una suite de pruebas automatizadas (unitarias e integrales), pruebas E2E y rendimiento, Pipeline CI/CD funcional, con estrategia de despliegue documentada, métricas de calidad y manual técnico. |

## V. Unidades de Aprendizaje

## Unidad 1: Fundamentos, Técnicas y Pruebas Unitarias de Software

| Resultado de aprendizaje | Producto |
|---|---|
| Aplica los fundamentos, técnicas y metodologías de pruebas de software para diseñar casos de prueba efectivos y gestionar el proceso de QA dentro del ciclo de vida del desarrollo. | **Nombre:** Plan de pruebas y casos de prueba documentados. |

| Criterios de evaluación del producto | Descripción del producto |
|---|---|
| Define el alcance y objetivos del plan de pruebas. Diseña casos de prueba usando técnicas de caja negra y caja blanca. Clasifica y prioriza defectos usando herramientas de gestión. Aplica pruebas de aceptación basadas en criterios del usuario. Elabora Plan de Pruebas considerando parte de los lineamientos IEEE 829 / ISO 29119. | Documento de plan de pruebas (IEEE 829/ISO 29119) que incluye estrategia, alcance, casos de prueba diseñados con técnicas formales, clasificación de defectos y criterios de aceptación; más suite de pruebas unitarias ejecutables con cobertura ≥ 70% sobre el módulo principal del proyecto. |

### Sesiones de aprendizaje

| N. | Fecha | Contenido | HT | HP | Actividad práctica | Actividad autónoma |
|---|---|---|---:|---:|---|---|
| 1 | 15/03/2026 - 21/03/2026 | ISOs de calidad de software. Norma técnica peruana y fundamentos de prueba: conceptos, principios, costo de los defectos y el rol del QA en el ciclo de vida del software (SDLC/STLC). | 2 | 2 | Analizar casos reales de fallos de software (Therac-25, Knight Capital). Mapear el ciclo SDLC/STLC en un proyecto de ejemplo e identificar el punto de mayor costo de defectos. | Lectura: cap. 1 de *The Art of Software Testing*. Elaborar un cuadro comparativo de ISO 25010 vs NTP ISO/IEC 25000 e identificar 3 métricas de calidad aplicables a un sistema bancario. |
| 2 | 22/03/2026 - 28/03/2026 | Tipos de pruebas: unitarias, integración, sistema y aceptación. Niveles de prueba, técnicas de diseño de pruebas (caja negra, caja blanca), pruebas estáticas (linters) y pruebas dinámicas. | 2 | 2 | Clasificar 15 escenarios de prueba en su tipo y nivel correspondiente. Diseñar la pirámide de testing para un e-commerce y justificar la proporción de cada nivel. | Investigar diferencias entre pruebas estáticas (ESLint, Checkstyle) y dinámicas. Proponer qué tipo de prueba y técnica aplicaría a cada módulo de su proyecto integrador. |
| 3 | 29/03/2026 - 04/04/2026 | Plan de Pruebas considerando parte de los lineamientos de la IEEE 829 / ISO 29119. Elaboración de casos de prueba. Herramientas de gestión: Jira, TestRail, TestLink. | 2 | 2 | Crear un Plan de Pruebas para un módulo de autenticación: alcance, criterios de entrada/salida, riesgos y cronograma. Diseñar 10 casos de prueba con partición equivalente y valores límite usando TestRail o TestLink. | Registrar y gestionar 5 defectos simulados en Jira con campos completos. Revisar la plantilla IEEE 829 y adaptar su estructura al proyecto del curso. |
| 4 | 05/04/2026 - 11/04/2026 | Pruebas unitarias, TDD, mocks, stubs y fixtures. | 2 | 2 | Implementar pruebas unitarias aplicando TDD: escribir la prueba primero, luego el código. Usar Mockito o unittest.mock para crear mocks y stubs. Alcanzar ≥ 70% de cobertura en el módulo asignado. | Leer sobre el patrón AAA y los principios FIRST para pruebas unitarias. Crear fixtures de prueba reutilizables para el proyecto integrador. Documentar qué decisiones de diseño facilitaron o dificultaron la prueba. |
| 5 | 12/04/2026 - 18/04/2026 | Evaluación Unidad 1. | 2 | 2 | Presentar el Plan de Pruebas completo con casos de prueba y suite de pruebas unitarias para el sistema asignado. Demostrar ejecución y reporte de cobertura. | Subsanar observaciones del evaluador, completar casos de prueba pendientes y preparar el repositorio para la Unidad 2. |

## Unidad 2: Pruebas Integrales, Automatización e Integración Continua

| Resultado de aprendizaje | Producto |
|---|---|
| Implementa suites de pruebas automatizadas utilizando frameworks modernos para pruebas unitarias, de integración y de interfaz de usuario, aplicando principios de diseño de pruebas mantenibles, y su ejecución con pipeline para la integración continua (CI). | **Nombre:** Informe sobre implementación de Pipeline de CI y Suite de pruebas automatizadas (unitarias, integración y E2E). |

| Criterios de evaluación del producto | Descripción del producto |
|---|---|
| Implementa pruebas unitarias con cobertura ≥ 80%. Configura mocks y stubs para pruebas de integración. Implementa pruebas E2E con Selenium o Cypress u otro similar. Aplica TDD y BDD (Gherkin/Cucumber) en al menos un módulo. Genera reportes de cobertura y resultados de pruebas. Implementa Pipeline de Integración continua. | Repositorio de código con suite de pruebas automatizadas unitarias, integración y E2E, más reporte de cobertura de código y documentación técnica de implementación de pipeline de integración continua (CI). |

### Sesiones de aprendizaje

| N. | Fecha | Contenido | HT | HP | Actividad práctica | Actividad autónoma |
|---|---|---|---:|---:|---|---|
| 1 | 19/04/2026 - 25/04/2026 | Automatización de pruebas: ventajas, desafíos, cuándo y qué automatizar, métricas de cobertura. | 2 | 2 | Escribir 10 pruebas unitarias parametrizadas con `@ParameterizedTest`. Medir cobertura con JaCoCo o Coverage.py y generar reporte HTML. Identificar módulos con cobertura menor a 60%. | Investigar la pirámide de pruebas y el concepto de flaky tests. Documentar qué módulos del proyecto son candidatos para automatizar primero y por qué, según ROI de automatización. |
| 2 | 26/04/2026 - 02/05/2026 | Pruebas de integración: BDD, mocks, stubs y test doubles con Mockito e inyección de dependencias. Pruebas de API REST con Postman. | 2 | 2 | Implementar pruebas de integración con Mockito: simular un repositorio de base de datos para probar la capa de servicio. Verificar interacciones y capturar argumentos. | Estudiar patrones de diseño aplicados en pruebas: Test Double, Fake, Spy. Refactorizar una clase del proyecto para aplicar inyección de dependencias y facilitar su prueba. |
| 3 | 03/05/2026 - 09/05/2026 | Configuración de ambientes de pruebas para integración continua: Docker, SonarQube, Jenkins y TestLink. GitHub Actions: workflows, triggers y jobs. | 2 | 2 | Configurar Docker Compose con la aplicación + SonarQube. Crear un workflow GitHub Actions que ejecute automáticamente pruebas unitarias, de integración y la colección Newman de API en cada push a main. | Comparar Jenkins vs GitHub Actions vs GitLab CI. Documentar el pipeline configurado con diagrama de fases, variables de entorno y criterios de fallo del build. |
| 4 | 10/05/2026 - 16/05/2026 | Ejecución de la suite completa de pruebas mediante el pipeline de integración continua. Análisis de calidad de código con SonarQube. Quality gates. | 2 | 2 | Ejecutar el pipeline completo en GitHub Actions. Analizar el reporte SonarQube e identificar y corregir al menos 3 issues críticos. Configurar un quality gate que falle el build si cobertura < 70%. | Investigar shift-left testing y su relación con integración continua. Proponer umbrales del quality gate del proyecto y justificarlos. |
| 5 | 17/05/2026 - 23/05/2026 | Pruebas de interfaz de usuario end-to-end (E2E): Selenium WebDriver y Cypress. Selectores CSS/XPath, Page Object Model y buenas prácticas. | 2 | 2 | Automatizar el flujo completo de un sistema web con Selenium WebDriver aplicando POM. Configurar ejecución headless e integrar E2E al pipeline GitHub Actions. | Comparar Selenium WebDriver vs Cypress vs Playwright. Documentar 5 selectores usados, su fragilidad potencial y mejoras con `data-testid`. |
| 6 | 24/05/2026 - 30/05/2026 | Revisión de pruebas de rendimiento y carga (Apache JMeter/k6) y seguridad (OWASP ZAP). | 2 | 2 | Generar reportes con JMeter (100 usuarios) y hallazgos de vulnerabilidad con OWASP ZAP. | Analizar los reportes de vulnerabilidad. |
| 7 | 31/05/2026 - 06/06/2026 | Evaluación Unidad II. | 2 | 2 | Demostrar el pipeline CI funcionando; presentar cobertura ≥ 80%, resultados API (Newman), E2E (Selenium/Cypress), reporte JMeter y hallazgos OWASP ZAP. | Subsanar observaciones del evaluador. Preparar documentación técnica final del repositorio: README, diagrama de arquitectura de la suite de pruebas y capturas de reportes. |

## Unidad 3: Integración y Despliegue Continuo (CI/CD)

| Resultado de aprendizaje | Producto |
|---|---|
| Configura e implementa pipelines de integración y entrega continua (CI/CD) aplicando estrategias de despliegue seguro, monitoreo post-despliegue y principios DevOps para garantizar la entrega confiable de software en producción. | **Nombre:** Pipeline CI/CD funcional con estrategia de despliegue documentado. |

| Criterios de evaluación del producto | Descripción del producto |
|---|---|
| Configura un pipeline CI/CD completo con Jenkins, GitHub Actions o GitLab CI. Integra la suite de pruebas automatizadas en el pipeline. Implementa análisis de calidad de código (SonarQube/SonarCloud). Documenta el pipeline y presenta sustentación técnica de implementación. Informe de ejecución de pruebas de software. | Pipeline CI/CD funcional que ejecute pruebas automáticas (unitarias, API, E2E), análisis de calidad SonarCloud, despliegue con estrategia Blue-Green o Canary, y documentación técnica completa. |

### Sesiones de aprendizaje

| N. | Fecha | Contenido | HT | HP | Actividad práctica | Actividad autónoma |
|---|---|---|---:|---:|---|---|
| 1 | 07/06/2026 - 13/06/2026 | Entrega continua (CD): ambientes Dev/QA/Staging/Prod. Gestión de artefactos. Docker: imágenes, contenedores, Dockerfile. | 2 | 2 | Containerizar la aplicación del proyecto con Docker: crear Dockerfile multi-stage, construir imagen y publicar en Docker Hub. Configurar Docker Compose con app + base de datos. Integrar build de imagen Docker al pipeline CI/CD. | Estudiar diferencias entre ambientes Dev, QA, Staging y Prod. Documentar la estrategia de gestión de artefactos y versionado de imágenes Docker con tags semánticos. |
| 2 | 14/06/2026 - 20/06/2026 | Presentación de informe de pruebas de software del proyecto final del curso. | 2 | 2 | Demostración en vivo: commit → build → test (unitarias + API + E2E) → quality gate → deploy (Blue-Green o Canary). | Entregar documentación técnica final: manual de operación del pipeline, runbook de incidentes, reporte consolidado de métricas de calidad y lecciones aprendidas. |
| 3 | 21/06/2026 - 27/06/2026 | Evaluación de Unidad 3. | 2 | 2 | Temas de todo el curso. | Adecuar mejoras dadas por el docente. |
| 4 | 28/06/2026 - 04/07/2026 | Estrategias de despliegue seguro: Blue-Green Deployment, Canary Release y Rolling Update. Análisis de calidad estática con SonarQube/SonarCloud integrado al pipeline. Gestión de secretos y variables de entorno en CI/CD. | 2 | 2 | Implementar estrategia Blue-Green con Docker Compose: configurar dos entornos, automatizar el switch de tráfico y verificar zero-downtime deployment. Agregar stage de SonarCloud al pipeline y configurar quality gate. | Comparar Blue-Green, Canary y Rolling. Diseñar plan de rollback del proyecto: triggers automáticos, RTO y pasos de reversión. |

## VI. Estrategias Metodológicas

| N. | Estrategias de enseñanza y de aprendizaje que se aplicarán en la asignatura |
|---|---|
| 1.1 | Aprendizaje Cooperativo: Fomenta habilidades colaborativas y de trabajo en equipo, cruciales en la mayoría de los entornos laborales modernos. |
| 1.2 | Aprendizaje Basado en Problemas: Centra el aprendizaje en la resolución de problemas reales, una habilidad esencial en casi todas las profesiones. Estimula el pensamiento crítico y la colaboración, elementos clave en el desarrollo de competencias. |
| 1.3 | Estudios de caso: Desarrolla el pensamiento crítico y la toma de decisiones al analizar situaciones complejas, preparando a los estudiantes para enfrentar problemas similares en sus futuras carreras profesionales. |

## VII. Recursos, Medios y Materiales

| N. | Recursos medios y materiales |
|---|---|
| 1 | Guías y/o tutoriales |
| 2 | Laboratorios |
| 3 | Internet - Wifi |
| 4 | Proyector y/o TV Smart |

## VIII. Evaluación

La evaluación de los estudiantes se rige por el Reglamento de Estudios, disponible en: <https://upeu.edu.pe/reglamentos/evaluacion>. La estructura evaluativa comprende componentes formativos y/o de procesos, de producto y genéricos, reflejando un enfoque integral.

| Fecha | Unidad | Producto | Evaluación de proceso y de resultado | Pesos |
|---|---|---|---|---:|
| 17/04/2026 | Unidad 1: Fundamentos, Técnicas y Pruebas Unitarias de Software | Plan de pruebas y casos de prueba documentados. | Evaluación de sesiones | 5% |
|  |  |  | Evaluación del producto | 20% |
| 05/06/2026 | Unidad 2: Pruebas Integrales, Automatización e Integración Continua | Informe sobre implementación de Pipeline de CI y Suite de pruebas automatizadas (unitarias, integración y E2E). | Evaluación de sesiones | 5% |
|  |  |  | Evaluación del producto | 20% |
| 03/07/2026 | Unidad 3: Integración y Despliegue Continuo (CI/CD) | Pipeline CI/CD funcional con estrategia de despliegue documentado. | Evaluación de sesiones | 10% |
|  |  |  | Evaluación del producto | 30% |
| 03/07/2026 | Competencia General | Carácter y aprendizaje autónomo. | Competencia General | 10% |

| Promedio ponderado de las evaluaciones | Pesos |
|---|---:|
| Evaluación de sesiones | 20% |
| Evaluación del producto | 70% |
| Evaluación de competencia genérica | 10% |
| Total | 100% |

## IX. Referencias

### Básica (Fuentes primarias)

- Aniche, M. (2022). *Effective Software Testing: A Developer's Guide*. Manning Publications.
- Humble, J., & Farley, D. (2010). *Continuous Delivery: Reliable Software Releases through Build, Test, and Deployment Automation*. Addison-Wesley.
- Hambling, B. (2019). *Software Testing*. 4Ed. BCS, The Chartered Institute for IT.
- Winters, T., Manshreck, T., & Wright, H. (2020). *Software Engineering at Google: Lessons Learned from Programming Over Time*. O'Reilly Media.
- Kim, G., Humble, J., Debois, P., & Willis, J. (2016). *The DevOps Handbook: How to Create World-Class Agility, Reliability, & Security in Technology Organizations*. IT Revolution Press.
- Myers, G. J., Sandler, C., & Badgett, T. (2011). *The Art of Software Testing* (3.ª ed.). Wiley.

### Complementaria (Fuentes secundarias)

- Beck, K. (2002). *Test-Driven Development: By Example*. Addison-Wesley Professional.
- Crispin, L., & Gregory, J. (2009). *Agile Testing: A Practical Guide for Testers and Agile Teams*. Addison-Wesley.
- Fowler, M. (2018). *Refactoring: Improving the Design of Existing Code* (2.ª ed.). Addison-Wesley.
- Neha, K. (2023). *Implementing Automated Software Testing*. Arcler Press.
- Nygard, M. T. (2018). *Release It!: Design and Deploy Production-Ready Software* (2.ª ed.). Pragmatic Bookshelf.
- Richardson, C. (2018). *Microservices Patterns: With Examples in Java*. Manning Publications.

### Enlaces de internet

- JMeter. Apache JMeter - Getting Started. <https://jmeter.apache.org/usermanual/get-started.html>
- Cypress. Why Cypress? <https://docs.cypress.io/guides/overview/why-cypress>
- JUnit. JUnit 5 User Guide. <https://junit.org/junit5/docs/current/user-guide/>
- GitHub. GitHub Actions Documentation. <https://docs.github.com/en/actions>
- International Software Testing Qualifications Board. ISTQB Certified Tester - Foundation Level Syllabus. <https://www.istqb.org>
- SonarSource. SonarCloud Documentation. <https://docs.sonarsource.com/sonarcloud/>
- Selenium. The Selenium Browser Automation Project. <https://www.selenium.dev/documentation/>
- Playwright. Getting Started. <https://playwright.dev/docs/intro>
