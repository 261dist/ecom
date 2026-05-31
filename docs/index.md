# DISTribuidas 2026

Curso de sistemas distribuidos basado en la construccion incremental de un sistema de microservicios con Spring Cloud.

El proyecto del curso es `ecom`: una plataforma distribuida con Config Server, Eureka, Gateway, microservicios Spring Boot, PostgreSQL, Kafka, observabilidad y frontend Angular.

## Producto del curso

Sistema distribuido basado en microservicios con Spring Cloud, seguro, configurable, resiliente, observable, orientado a eventos, integrado con frontend y defendido tecnicamente.

## Unidades

| Unidad | Producto |
|---|---|
| U1 | Sistema distribuido base con Spring Cloud |
| U2 | Sistema distribuido robusto e integrado |
| U3 | Producto final del curso validado, documentado y defendido |

## Sesiones

| Sesion | Tema | Producto de sesion |
|---|---|---|
| S1 | Arquitectura base de microservicios | Estructura base del sistema y primeros microservicios ejecutables |
| S2 | Configuracion centralizada | Config Server con perfiles `dev` y `prod` |
| S3 | Eureka y escalado | Servicios registrados y multiples instancias operativas |
| S4 | Gateway y balanceo | Punto unico de acceso con rutas y load balancing |
| S5 | Evaluacion U1 | Sistema base integrado funcionando como un todo |
| S6 | OpenFeign | Comunicacion entre microservicios |
| S7 | Circuit Breaker | Resiliencia y fallback ante fallos |
| S8 | Seguridad JWT | Login, token y rutas protegidas |
| S9 | Kafka | Arquitectura orientada a eventos |
| S10 | Observabilidad consolidada | Logs, health, metricas y paneles de diagnostico |
| S11 | Angular + Gateway | Frontend integrado con CORS, login y CRUD |
| S12 | Evaluacion U2 | Sistema robusto validado en condiciones reales |
| S13 | Validacion integral | Producto del curso probado end-to-end |
| S14 | Cierre tecnico | Documentacion, evidencias y estabilizacion |
| S15 | Defensa tecnica | Sustentacion grupal del producto |
| S16 | Evaluacion final | Demostracion individual de competencias pendientes |

## Regla del curso

Cada sesion produce un avance verificable del producto de unidad.

No basta con que compile. El estudiante debe poder levantar, probar, inspeccionar, diagnosticar y defender el sistema.

## Convencion de trabajo

- Windows: PowerShell.
- macOS/Linux: bash con `curl`.
- Pruebas de API: shell contra el Gateway, no Postman como dependencia obligatoria.
- Swagger: solo directo al puerto asignado de cada microservicio.
- Observabilidad: eje transversal desde S2, consolidado en S10.

## Primeros enlaces

- [Guia del curso](guia-curso.md)
- [Puertos y accesos](referencias/puertos.md)
- [Comandos PowerShell](referencias/comandos-powershell.md)
- [Comandos bash macOS/Linux](referencias/comandos-bash.md)
- [Troubleshooting](referencias/troubleshooting.md)
- [Rubrica](referencias/rubrica.md)
