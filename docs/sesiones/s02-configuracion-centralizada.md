# S2 - Configuracion centralizada

## Ubicacion en el curso

- Unidad: U1 - Sistema distribuido base con Spring Cloud.
- Producto de unidad: Sistema distribuido base configurable, registrado, accesible por Gateway y preparado para multiples instancias.
- Avance del producto en esta sesion: Config Server operativo con perfiles `dev` y `prod`.

## Proposito

Externalizar la configuracion para evitar valores embebidos en cada microservicio y mantener consistencia entre entornos.

## Resultado de aprendizaje

El estudiante levanta Config Server, consulta configuraciones por perfil y explica como los microservicios cargan configuracion externa.

## Producto de sesion

- Config Server operativo.
- Repositorio de configuracion visible por HTTP.
- Configuracion `dev` y `prod` consultable por servicio.

## Concepto distribuido clave

La configuracion centralizada permite cambiar parametros de entorno sin recompilar servicios. Es una base para operar sistemas distribuidos en multiples ambientes.

## Implementacion en el proyecto

Config Server vive en `infra/config` y publica archivos desde `infra/config/config-repo`.

## Pasos para construir el producto de sesion

1. Crear el proyecto `infra/config` con Spring Cloud Config Server.
2. Habilitar Config Server con la anotacion correspondiente en la aplicacion principal.
3. Configurar el repositorio nativo de archivos de configuracion.
4. Crear archivos por microservicio y perfil: `servicio-dev.yml` y `servicio-prod.yml`.
5. Mover puertos, credenciales, Eureka y propiedades de observabilidad fuera del codigo del microservicio.
6. Configurar cada microservicio para importar configuracion desde Config Server.
7. Levantar Config Server y consultar `/{application}/{profile}` desde navegador o shell.
8. Verificar que un microservicio arranca usando valores externos.

## Archivos involucrados

| Archivo | Proposito |
|---|---|
| `infra/config/src/main/resources/application.yml` | Configuracion del Config Server |
| `infra/config/config-repo/*-dev.yml` | Configuracion DEV |
| `infra/config/config-repo/*-prod.yml` | Configuracion PROD |
| `services/*/src/main/resources/application.yml` | Importa Config Server |

## Comandos de ejecucion

### PowerShell

```powershell
cd infra/config
mvn spring-boot:run
```

### bash macOS/Linux

```bash
cd infra/config
mvn spring-boot:run
```

## Verificacion funcional

```text
http://localhost:18888/producto-ms/dev
http://localhost:18888/catalogo-ms/dev
```

## Observabilidad y diagnostico

- Health: `http://localhost:18888/actuator/health`.
- Revisar logs de lectura del repositorio de configuracion.
- Validar que el perfil consultado exista.

## Verificacion de base de datos

No aplica directamente. La sesion valida configuracion de conexion, no registros.

## Evidencia esperada

- Captura o salida JSON/YAML de Config Server.
- Explicacion de diferencias entre `dev` y `prod`.

## Errores frecuentes

| Problema | Causa probable | Solucion |
|---|---|---|
| 404 al consultar config | Nombre de servicio incorrecto | Usar `spring.application.name` |
| No carga config | Config Server apagado | Levantar `infra/config` |

## Preguntas de defensa

1. Que problema resuelve Config Server?
2. Por que conviene separar perfiles `dev` y `prod`?
3. Que pasa si un microservicio arranca sin Config Server?

## Checklist de cierre

- [ ] Config Server responde health.
- [ ] Consulto configuracion DEV.
- [ ] Consulto configuracion PROD.
- [ ] Explico la carga de configuracion externa.
