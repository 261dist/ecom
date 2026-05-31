# S3 - Registro, descubrimiento y escalado

## Ubicacion en el curso

- Unidad: U1 - Sistema distribuido base con Spring Cloud.
- Producto de unidad: Sistema distribuido base configurable, registrado, accesible por Gateway y preparado para multiples instancias.
- Avance del producto en esta sesion: servicios registrados dinamicamente y multiples instancias activas.

## Proposito

Incorporar service discovery para que los servicios no dependan de direcciones fijas y puedan escalar en multiples instancias.

## Resultado de aprendizaje

El estudiante registra microservicios en Eureka y ejecuta mas de una instancia del mismo servicio.

## Producto de sesion

- Eureka Server operativo.
- Servicios registrados.
- Dos instancias de un microservicio visibles en Eureka.

## Concepto distribuido clave

Service discovery permite localizar servicios por nombre logico, no por IP o puerto. Es clave para escalado y tolerancia a cambios de instancia.

## Implementacion en el proyecto

Eureka vive en `infra/eureka`. Los microservicios usan `eureka.client.service-url.defaultZone` desde Config Server.

## Pasos para construir el producto de sesion

1. Crear el proyecto `infra/eureka` con Spring Cloud Netflix Eureka Server.
2. Habilitar Eureka Server en la clase principal.
3. Configurar el puerto DEV de Eureka.
4. Agregar dependencias de Eureka Client en los microservicios.
5. Definir `spring.application.name` para cada microservicio.
6. Configurar `eureka.client.service-url.defaultZone` desde Config Server.
7. Configurar `server.port: 0` en DEV para permitir multiples instancias.
8. Levantar dos instancias del mismo microservicio y validar ambas en Eureka.

## Archivos involucrados

| Archivo | Proposito |
|---|---|
| `infra/eureka/src/main/resources/application.yml` | Configuracion Eureka |
| `infra/config/config-repo/*-dev.yml` | Registro de servicios en DEV |
| `services/*/src/main/resources/application.yml` | Nombre de aplicacion |

## Comandos de ejecucion

### PowerShell

```powershell
cd infra/eureka
mvn spring-boot:run

cd services/catalogo-ms
mvn spring-boot:run
```

Segunda instancia:

```powershell
cd services/catalogo-ms
mvn spring-boot:run
```

### bash macOS/Linux

```bash
cd infra/eureka
mvn spring-boot:run

cd services/catalogo-ms
mvn spring-boot:run
```

## Verificacion funcional

```text
http://localhost:18761
```

Debe aparecer `CATALOGO-MS` con una o mas instancias.

## Observabilidad y diagnostico

- Revisar dashboard Eureka.
- Revisar logs de registro del cliente.
- Verificar `instance-id` y puerto dinamico.

## Verificacion de base de datos

No aplica, salvo que el microservicio requiera BD para arrancar.

## Evidencia esperada

- Captura de Eureka con servicios registrados.
- Dos instancias del mismo servicio.

## Errores frecuentes

| Problema | Causa probable | Solucion |
|---|---|---|
| Servicio no aparece | Eureka apagado | Levantar `infra/eureka` |
| Solo aparece una instancia | Se ejecuto una sola terminal | Abrir segunda terminal |

## Preguntas de defensa

1. Por que Eureka mejora el desacoplamiento?
2. Que cambia al ejecutar dos instancias?
3. Que informacion muestra Eureka de cada instancia?

## Checklist de cierre

- [ ] Eureka esta activo.
- [ ] Un microservicio aparece registrado.
- [ ] Una segunda instancia aparece registrada.
- [ ] Explico service discovery.
