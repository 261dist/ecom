# S1 - Arquitectura base de microservicios

## Ubicacion en el curso

- Unidad: U1 - Sistema distribuido base con Spring Cloud.
- Producto de unidad: Sistema distribuido base configurable, registrado, accesible por Gateway y preparado para multiples instancias.
- Avance del producto en esta sesion: estructura inicial del sistema y microservicios stateless ejecutables.

## Proposito

Organizar el sistema `ecom` como una plataforma distribuida con responsabilidades separadas y bases de datos independientes por microservicio.

## Resultado de aprendizaje

El estudiante identifica los componentes del sistema, levanta servicios base y explica por que un microservicio debe ser stateless, configurable y reemplazable.

## Producto de sesion

- Monorepo reconocido y navegable.
- Microservicios identificados por responsabilidad.
- PostgreSQL DEV levantado para los servicios principales.
- Primer servicio ejecutado con Maven.

## Concepto distribuido clave

Un sistema distribuido separa capacidades en servicios independientes que se comunican por red. La independencia permite escalar, reemplazar y desplegar partes del sistema sin mover todo el producto.

## Implementacion en el proyecto

Se revisa la estructura:

```text
infra/
services/
clients/
kafka/
obs/
docs/
```

## Pasos para construir el producto de sesion

1. Crear o revisar la estructura del monorepo separando `infra`, `services`, `clients`, `kafka`, `obs` y `docs`.
2. Definir la responsabilidad de cada microservicio antes de escribir codigo.
3. Crear un microservicio Spring Boot por capacidad del dominio.
4. Asignar una base de datos propia a cada microservicio.
5. Crear `compose-dev.yml` para levantar solo la BD del servicio en desarrollo.
6. Configurar el microservicio como stateless: sin estado de sesion local ni dependencia de archivos temporales.
7. Ejecutar el microservicio con Maven y confirmar que puede iniciar de forma independiente.
8. Documentar en el README del servicio como levantarlo, probarlo e inspeccionar su BD.

## Archivos involucrados

| Archivo | Proposito |
|---|---|
| `README.md` | Entrada operativa del repositorio |
| `services/*/README.md` | Guia por microservicio |
| `services/*/compose-dev.yml` | PostgreSQL DEV por servicio |
| `services/*/pom.xml` | Dependencias Java |

## Comandos de ejecucion

### PowerShell

```powershell
docker network create ecom-dev-net
cd services/catalogo-ms
docker compose -f compose-dev.yml up -d
mvn spring-boot:run
```

### bash macOS/Linux

```bash
docker network create ecom-dev-net
cd services/catalogo-ms
docker compose -f compose-dev.yml up -d
mvn spring-boot:run
```

## Verificacion funcional

El microservicio arranca sin errores y muestra en consola el puerto asignado.

## Observabilidad y diagnostico

- Revisar logs de arranque.
- Identificar puerto asignado por `server.port: 0`.
- Confirmar conexion a PostgreSQL.

## Verificacion de base de datos

```powershell
docker exec -it ecom-postgres-catalogo-dev psql -U ecom -d ecom_catalogo_db -c "\dt"
```

## Evidencia esperada

- Captura o salida de consola con el servicio iniciado.
- Contenedor PostgreSQL DEV activo.
- Explicacion de la responsabilidad de cada carpeta.

## Errores frecuentes

| Problema | Causa probable | Solucion |
|---|---|---|
| El puerto ya esta ocupado | Servicio anterior activo | Revisar procesos o usar puerto dinamico |
| No conecta a BD | PostgreSQL DEV no levantado | Ejecutar `docker compose -f compose-dev.yml up -d` |

## Preguntas de defensa

1. Por que cada microservicio tiene su propia base de datos?
2. Que significa que un microservicio sea stateless?
3. Que ventaja tiene usar puerto dinamico en DEV?

## Checklist de cierre

- [ ] Identifico la estructura del sistema.
- [ ] Levanto una BD DEV.
- [ ] Ejecuto un microservicio con Maven.
- [ ] Explico el rol del microservicio ejecutado.
