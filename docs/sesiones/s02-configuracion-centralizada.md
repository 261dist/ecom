# S2 - Gestion centralizada de configuracion y ambientes

## 1. Introduccion

Tiempo: 20 min.

### 1.1 Proposito

Centralizar la configuracion del sistema para separar el codigo de los valores de ambiente y preparar a los microservicios para ejecutarse de forma consistente en DEV y PROD local.

### 1.2 Resultado de aprendizaje

El estudiante implementa un servidor de configuracion centralizada, publica configuraciones por servicio y perfil, consulta esas configuraciones por HTTP y verifica que un microservicio puede arrancar usando valores externos.

### 1.3 Producto de sesion

Config Server operativo en `infra/config`, con `config-repo` local, perfiles `dev` y `prod`, consultas HTTP verificadas y al menos un microservicio leyendo configuracion externa.

### 1.4 Motivacion de la sesion

#### 1.4.1 Caso: configuracion duplicada entre servicios

En la sesion anterior se construyo `catalogo-ms` como microservicio base. Al crecer el sistema aparecen nuevos servicios como `producto-ms`, `orden-ms`, `pago-ms` y componentes de infraestructura.

Si cada proyecto guarda sus propios puertos, credenciales, rutas, perfiles y opciones de observabilidad, aparecen problemas:

- Cambios repetidos en muchos archivos.
- Diferencias accidentales entre DEV y PROD local.
- Credenciales o rutas hardcodeadas.
- Dificultad para saber que configuracion usa cada servicio.
- Mayor riesgo de errores cuando se levantan varias instancias.

La pregunta que guia esta sesion es:

```text
Como hacemos que los servicios lean su configuracion desde un punto central sin recompilar ni duplicar valores?
```

### 1.5 Ubicacion en el curso

- Unidad: U1 - Sistema distribuido base orientado a produccion.
- Producto de unidad: sistema distribuido base funcional, configurable y preparado para multiples instancias.
- Avance del producto en esta sesion: configuracion externa por ambiente mediante Config Server.

Roadmap para elaborar el producto de la unidad:

```mermaid
flowchart TB
    Cliente["Cliente de prueba<br/>PowerShell / bash / Swagger"]
    Gateway["Gateway<br/>punto unico de acceso<br/>balanceo de carga"]
    Catalogo["catalogo-ms<br/>construido<br/>REST + BD + health"]
    Producto["producto-ms<br/>trabajo aplicado"]
    Eureka["Registro de servicios<br/>Eureka"]
    Config["Servidor de configuracion<br/>Config Server<br/>HOY"]
    Repo["Repositorio de configuracion<br/>catalogo-ms.yml<br/>producto-ms.yml<br/>HOY"]

    Cliente --> Gateway
    Gateway --> Catalogo
    Gateway --> Producto
    Gateway -. descubre servicios .-> Eureka
    Catalogo -. registra instancia .-> Eureka
    Producto -. registra instancia .-> Eureka
    Catalogo -. carga configuracion .-> Config
    Producto -. carga configuracion .-> Config
    Config --> Repo

    classDef done fill:#e8f5e9,stroke:#2e7d32,color:#111;
    classDef today fill:#ffe08a,stroke:#9a6b00,stroke-width:2px,color:#111;
    class Catalogo done;
    class Config,Repo today;
```

## 2. Explica

Tiempo: 15 min.

### 2.1 Conceptos clave

La configuracion centralizada permite que los servicios obtengan valores de ambiente desde un servidor comun. Asi el codigo queda separado de valores como puertos, URLs, credenciales, rutas, niveles de log y opciones de observabilidad.

Conceptos de la sesion:

- **Config Server**: componente que entrega configuracion por HTTP.
- **Config repo**: repositorio o carpeta donde viven los archivos `*.yml` de configuracion.
- **Perfil**: variante de configuracion, por ejemplo `dev` o `prod`.
- **Nombre de aplicacion**: identificador usado para buscar el archivo correcto, por ejemplo `catalogo-ms`.
- **Config Client**: aplicacion que lee su configuracion desde Config Server.

Convencion de archivos:

```text
{application-name}-{profile}.yml
```

Ejemplos:

```text
catalogo-ms-dev.yml
catalogo-ms-prod.yml
producto-ms-dev.yml
producto-ms-prod.yml
```

### 2.2 Arquitectura del producto en `ecom`

En `ecom`, Config Server vive en:

```text
infra/config
```

El repositorio local de configuracion vive dentro del mismo proyecto para simplificar el laboratorio:

```text
infra/config/config-repo
```

Aunque fisicamente `config-repo` esta dentro de `infra/config`, logicamente son responsabilidades distintas:

- Config Server atiende peticiones HTTP.
- Config repo almacena archivos de configuracion.

#### 2.2.1 Configuracion en DEV

```mermaid
flowchart LR
    Client["Cliente<br/>PowerShell / bash / navegador"]
    Config["ecom-config<br/>Config Server<br/>infra/config<br/>localhost:18888"]
    Repo["file:./config-repo<br/>catalogo-ms-dev.yml<br/>catalogo-ms-prod.yml<br/>producto-ms-dev.yml<br/>producto-ms-prod.yml"]
    Catalogo["catalogo-ms"]
    Producto["producto-ms"]

    Client -->|"GET localhost:18888/catalogo-ms/dev"| Config
    Client -->|"GET localhost:18888/producto-ms/dev"| Config
    Config -->|"lee archivos"| Repo
    Catalogo -. "spring.config.import<br/>http://localhost:18888" .-> Config
    Producto -. "spring.config.import<br/>http://localhost:18888" .-> Config

    classDef server fill:#eef6ff,stroke:#2b6cb0,color:#111;
    classDef repo fill:#fff4de,stroke:#b7791f,color:#111;
    class Config,Catalogo,Producto server;
    class Repo repo;
```

En DEV, Config Server corre con Maven en el host:

```text
localhost:18888
config-repo: file:./config-repo
```

#### 2.2.2 Configuracion en PROD local

```mermaid
flowchart LR
    Client["Cliente<br/>PowerShell / bash"]
    subgraph Docker["Docker Network: ecom-prod-net"]
        Config["ecom-config<br/>Config Server<br/>8888 interno"]
        Repo["file:/config-repo<br/>catalogo-ms-prod.yml<br/>producto-ms-prod.yml"]
        Catalogo["catalogo-ms"]
        Producto["producto-ms"]
    end

    Client -->|"GET localhost:28888/catalogo-ms/prod"| Config
    Client -->|"GET localhost:28888/producto-ms/prod"| Config
    Config -->|"lee archivos"| Repo
    Catalogo -. "spring.config.import<br/>http://ecom-config:8888" .-> Config
    Producto -. "spring.config.import<br/>http://ecom-config:8888" .-> Config

    classDef server fill:#eef6ff,stroke:#2b6cb0,color:#111;
    classDef repo fill:#fff4de,stroke:#b7791f,color:#111;
    class Config,Catalogo,Producto server;
    class Repo repo;
```

En PROD local, Config Server corre como contenedor:

```text
host: localhost:28888
docker interno: ecom-config:8888
CONFIG_REPO_LOCATION=file:/config-repo
```

#### 2.2.3 Estado nuevo de URLs en S2

Las URLs de esta sesion corresponden al monorepo `ecom` nuevo. No se usan los puertos ni nombres del sistema anterior.

| Ambiente | Componente | URL o nombre |
|---|---|---|
| DEV | Config Server | `http://localhost:18888` |
| DEV | Config de catalogo | `http://localhost:18888/catalogo-ms/dev` |
| DEV | Config de producto | `http://localhost:18888/producto-ms/dev` |
| DEV | `catalogo-ms` | `http://localhost:<puerto-dinamico>` |
| PROD local | Config Server desde host | `http://localhost:28888` |
| PROD local | Config Server desde contenedores | `http://ecom-config:8888` |
| PROD local | Config de catalogo | `http://localhost:28888/catalogo-ms/prod` |
| PROD local | Config de producto | `http://localhost:28888/producto-ms/prod` |
| PROD local | `catalogo-ms` dentro de Docker | `http://catalogo-ms:8080` |

Ejemplos que pertenecen al sistema anterior, como `localhost:7071`, `localhost:7072`, `localhost:8081`, `localhost:8082`, `/catalogo/dev` o `/catalogo/prod`, no se usan como rutas validas del sistema nuevo.

### 2.3 Observabilidad y diagnostico

En esta sesion la observabilidad se enfoca en confirmar que Config Server esta activo y que entrega la configuracion esperada.

#### 2.3.1 Senales basicas a revisar

- Health de Config Server.
- Metricas basicas de Config Server.
- Logs de arranque.
- Ruta del `config-repo`.
- Perfil consultado.
- Nombre de aplicacion consultado.
- Diferencias entre `dev` y `prod`.

#### 2.3.2 Errores frecuentes y diagnostico

| Problema | Causa probable | Solucion |
|---|---|---|
| 404 al consultar configuracion | Nombre de aplicacion o perfil incorrecto | Revisar nombre del archivo `{app}-{profile}.yml` |
| Config Server no encuentra archivos | `search-locations` incorrecto | En DEV revisar `file:./config-repo`; en PROD revisar `CONFIG_REPO_LOCATION` |
| Microservicio arranca con valores locales | No importa Config Server | Revisar `spring.config.import` |
| Microservicio no arranca | Config Server apagado o URL incorrecta | Levantar Config Server y revisar `CONFIG_SERVER_URL` |
| Se consulta `prod` pero aparecen valores de `dev` | Perfil activo incorrecto | Revisar `SPRING_PROFILES_ACTIVE` |

## 3. Aplica: actividad practica guiada

En el laboratorio, el docente guia la construccion del Config Server y la externalizacion de configuracion de `catalogo-ms`. Los estudiantes verifican la configuracion por HTTP y luego repiten el patron con `producto-ms`.

Tiempo: 3h.

La ruta principal de la sesion es construir desde cero. Si el estudiante necesita avanzar mas rapido, puede usar la ruta alternativa del paso 3.17 para clonar el tag final y ejecutar las pruebas.

- Crear la base de infraestructura.
- Crear el proyecto `ecom-config`.
- Crear `config-repo` dentro de `infra/config`.
- Mover configuraciones `dev` y `prod` al repositorio de configuracion.
- Conectar `catalogo-ms` como Config Client.
- Probar `catalogo-ms` en DEV y PROD local.
- Repetir el patron con `producto-ms`.

### 3.1 Crear la base `infra`

**Producto del paso:** carpeta `infra` preparada para alojar componentes de infraestructura del sistema.

En `ecom`, la infraestructura se trabaja dentro del monorepo. Si construyes desde cero, ubicate en la raiz del proyecto y crea la carpeta:

PowerShell / bash macOS/Linux:

```bash
mkdir infra
```

En esta version del curso trabajaremos todo desde `ecom`. La opcion de clonar un avance ya terminado queda separada en la ruta alternativa del paso 3.17.

Estructura esperada al iniciar la sesion:

```text
ecom
  infra/
  services/
    catalogo-ms/
    producto-ms/
```

### 3.2 Crear proyecto Config Server

**Producto del paso:** proyecto Spring Boot `ecom-config` creado dentro de `infra/config`.

Desde VS Code, usa Spring Initializr:

```text
Spring Initializr: Create a Maven Project
```

Configuracion del proyecto:

| Campo | Valor |
|---|---|
| Project | Maven Project |
| Spring Boot | 3.5.x |
| Language | Java |
| Java | 17 |
| Group Id | `com.upeu` |
| Artifact Id | `ecom-config` |
| Package name | `com.upeu.configserver` |
| Packaging | Jar |
| Ubicacion | `infra/config` |

Dependencias Spring Boot:

| Grupo | Dependencias | Proposito |
|---|---|---|
| Spring Cloud | Config Server | Entregar configuracion externa por HTTP |
| Operacion | Spring Boot Actuator | Verificar health del servidor |
| Productividad | Spring Boot DevTools | Facilitar ejecucion en desarrollo |

En S2 aparece Spring Cloud por primera vez. En esta sesion solo usamos Config Server; Eureka, Gateway y Load Balancer se integran en las sesiones siguientes.

En `pom.xml`, la dependencia clave es:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-config-server</artifactId>
</dependency>
```

### 3.3 Habilitar Config Server

**Producto del paso:** aplicacion Spring Boot marcada como servidor de configuracion.

En la clase principal agrega `@EnableConfigServer`:

```java
package com.upeu.configserver;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.config.server.EnableConfigServer;

@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {

    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}
```

### 3.4 Crear `config-repo` dentro de `infra/config`

**Producto del paso:** repositorio local de configuracion creado dentro del proyecto Config Server.

PowerShell / bash macOS/Linux:

```bash
mkdir infra/config/config-repo
```

En esta version del curso, `config-repo` vive dentro de `infra/config` para reducir dispersion de archivos durante el laboratorio local.

Conceptualmente siguen siendo dos responsabilidades distintas:

```text
Config Server -> entrega configuracion por HTTP
config-repo   -> almacena archivos YAML por servicio y ambiente
```

### 3.5 Configurar Config Server para leer `config-repo`

**Producto del paso:** Config Server configurado para leer archivos desde `infra/config/config-repo` en DEV.

En `infra/config/src/main/resources/application.yml`:

```yaml
server:
  port: 18888

spring:
  application:
    name: ecom-config
  profiles:
    active: native
  cloud:
    config:
      server:
        native:
          search-locations: ${CONFIG_REPO_LOCATION:file:./config-repo}

management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics
  endpoint:
    health:
      show-details: always
```

En DEV no se define variable de entorno. Se usa el valor por defecto:

```text
file:./config-repo
```

Eso significa que debes ejecutar Maven parado en:

```text
infra/config
```

En PROD local si se usara variable de entorno, porque el repositorio se monta dentro del contenedor como `/config-repo`.

### 3.6 Probar Config Server en DEV

**Producto del paso:** Config Server ejecutando en `localhost:18888`.

PowerShell / bash macOS/Linux:

```bash
cd infra/config
mvn spring-boot:run
```

Verifica health:

PowerShell:

```powershell
Invoke-RestMethod `
  -Method Get `
  -Uri "http://localhost:18888/actuator/health"
```

bash macOS/Linux:

```bash
curl http://localhost:18888/actuator/health
```

Verifica metrics:

PowerShell:

```powershell
Invoke-RestMethod `
  -Method Get `
  -Uri "http://localhost:18888/actuator/metrics"
```

bash macOS/Linux:

```bash
curl http://localhost:18888/actuator/metrics
```

### 3.7 Crear archivos de configuracion en `config-repo`

**Producto del paso:** configuraciones `dev` y `prod` creadas para `catalogo-ms`.

Crea estos archivos:

```text
infra/config/config-repo/catalogo-ms-dev.yml
infra/config/config-repo/catalogo-ms-prod.yml
```

Regla de nombres:

```text
{spring.application.name}-{profile}.yml
```

Ejemplo para DEV:

```yaml
server:
  port: 0

spring:
  datasource:
    url: jdbc:postgresql://localhost:15432/ecom_catalogo_db
    username: ecom
    password: ecom
    driver-class-name: org.postgresql.Driver
  flyway:
    enabled: true
    locations: classpath:db/migration
  jpa:
    hibernate:
      ddl-auto: validate
    show-sql: true
    properties:
      hibernate:
        format_sql: true

springdoc:
  swagger-ui:
    path: /swagger-ui.html

logging:
  level:
    com.upeu.catalogo: DEBUG

management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics
  endpoint:
    health:
      show-details: always
```

Ejemplo para PROD local:

```yaml
server:
  port: 8080

spring:
  datasource:
    url: jdbc:postgresql://${DB_HOST}:${DB_PORT}/${DB_NAME}
    username: ${DB_USER}
    password: ${DB_PASS}
    driver-class-name: org.postgresql.Driver
  flyway:
    enabled: true
    locations: classpath:db/migration
  jpa:
    hibernate:
      ddl-auto: validate
    show-sql: false
    properties:
      hibernate:
        format_sql: false

springdoc:
  swagger-ui:
    enabled: false
  api-docs:
    enabled: false

management:
  endpoints:
    web:
      exposure:
        include: health,info
  endpoint:
    health:
      show-details: never
```

### 3.8 Consultar perfiles por HTTP

**Producto del paso:** configuracion externa consultada sin levantar el microservicio.

Con Config Server ejecutando en DEV:

PowerShell / bash macOS/Linux:

```bash
curl http://localhost:18888/catalogo-ms/dev
curl http://localhost:18888/catalogo-ms/prod
```

Si usas PowerShell y prefieres objetos:

```powershell
Invoke-RestMethod `
  -Method Get `
  -Uri "http://localhost:18888/catalogo-ms/dev"
```

Resultado esperado:

- La respuesta debe indicar `name: catalogo-ms`.
- La respuesta debe indicar `profiles: ["dev"]`.
- En `propertySources` debe aparecer un archivo parecido a `file:.../infra/config/config-repo/catalogo-ms-dev.yml`.
- Dentro de `source` deben verse propiedades como `server.port`, `spring.datasource.url`, `spring.flyway.enabled`, `spring.jpa.hibernate.ddl-auto`, `springdoc.swagger-ui.path` y `management.endpoints.web.exposure.include`.

Ejemplo resumido del resultado:

```json
{
  "name": "catalogo-ms",
  "profiles": ["dev"],
  "propertySources": [
    {
      "name": "file:.../config-repo/catalogo-ms-dev.yml",
      "source": {
        "server.port": 0,
        "spring.datasource.url": "jdbc:postgresql://localhost:15432/ecom_catalogo_db",
        "spring.flyway.enabled": true,
        "spring.jpa.hibernate.ddl-auto": "validate",
        "springdoc.swagger-ui.path": "/swagger-ui.html",
        "management.endpoints.web.exposure.include": "health,info,metrics,prometheus"
      }
    }
  ]
}
```

Si Config Server no muestra esas propiedades, no continues a PROD. Primero corrige el nombre del archivo, el perfil o la ubicacion de `config-repo`.

#### 3.8.1 Probar una consulta incorrecta para aprender del error

Ahora consulta un nombre que no coincide con `spring.application.name` ni con el archivo del `config-repo`.

PowerShell / bash macOS/Linux:

```bash
curl http://localhost:18888/catalogo/dev
```

Resultado esperado:

- La consulta no debe devolver la configuracion de `catalogo-ms-dev.yml`.
- Puede responder sin `propertySources` utiles o con una respuesta vacia segun la configuracion del servidor.
- El error conceptual es que `catalogo` no coincide con `catalogo-ms`.

La regla que debe quedar clara:

```text
spring.application.name = catalogo-ms
archivo esperado       = catalogo-ms-dev.yml
URL correcta           = /catalogo-ms/dev
URL incorrecta         = /catalogo/dev
```

Este error controlado ayuda a diagnosticar uno de los problemas mas comunes en Config Server: el servicio arranca o consulta una configuracion que no corresponde porque el nombre de aplicacion y el nombre del archivo no coinciden.

### 3.9 Conectar `catalogo-ms` como Config Client

**Producto del paso:** `catalogo-ms` preparado para consumir configuracion externa en DEV.

Este paso tiene dos cambios: agregar Config Client al microservicio y mover sus archivos de ambiente hacia `config-repo`.

Agrega tres configuraciones en `services/catalogo-ms/pom.xml`.

1. Declarar la version de Spring Cloud en `<properties>`:

```xml
<properties>
    <java.version>17</java.version>
    <spring-cloud.version>2025.0.1</spring-cloud.version>
</properties>
```

2. Agregar la dependencia de Config Client en `<dependencies>`:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
```

3. Agregar el BOM de Spring Cloud en `<dependencyManagement>`:

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>${spring-cloud.version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

Luego deja `services/catalogo-ms/src/main/resources/application.yml` solo con configuracion base e importacion del Config Server:

```yaml
spring:
  application:
    name: catalogo-ms
  profiles:
    active: dev
  config:
    import: "optional:configserver:${CONFIG_SERVER_URL:http://localhost:18888}"
```

Mueve la configuracion que antes estaba en `application-dev.yml` y `application-prod.yml` hacia:

```text
infra/config/config-repo/catalogo-ms-dev.yml
infra/config/config-repo/catalogo-ms-prod.yml
```

En DEV se usa `http://localhost:18888`. En PROD local se usara `CONFIG_SERVER_URL=http://ecom-config:8888`.

La URL no lleva usuario ni password porque el Config Server actual no tiene seguridad habilitada. Si luego se agrega seguridad basica al Config Server, la URL cambiaria a un formato como `http://usuario:password@host:puerto`.

### 3.10 Levantar `catalogo-ms` en DEV con Config Server

**Producto del paso:** `catalogo-ms` ejecutando con valores entregados por Config Server.

Terminal 1:

```bash
cd infra/config
mvn spring-boot:run
```

Terminal 2:

```bash
cd services/catalogo-ms
docker compose -f compose-dev.yml up -d
mvn spring-boot:run
```

Verifica en logs:

- Nombre de aplicacion `catalogo-ms`.
- Perfil `dev`.
- Puerto dinamico.
- Conexion a PostgreSQL.
- Configuracion recibida desde Config Server.

Luego prueba que `catalogo-ms` sigue funcionando. Como el puerto es dinamico, toma el puerto asignado desde la consola de Spring Boot. En los ejemplos se usa `<puerto>`.

PowerShell:

```powershell
Invoke-RestMethod `
  -Method Get `
  -Uri "http://localhost:<puerto>/actuator/health"

Invoke-RestMethod `
  -Method Get `
  -Uri "http://localhost:<puerto>/actuator/metrics"

Invoke-RestMethod `
  -Method Get `
  -Uri "http://localhost:<puerto>/api/v1/categorias"
```

bash macOS/Linux:

```bash
curl http://localhost:<puerto>/actuator/health
curl http://localhost:<puerto>/actuator/metrics
curl http://localhost:<puerto>/api/v1/categorias
```

Tambien revisa Swagger desde el navegador:

```text
http://localhost:<puerto>/swagger-ui.html
```

Resultado esperado:

- `/actuator/health` responde `UP`.
- `/actuator/metrics` responde la lista de metricas disponibles.
- `/api/v1/categorias` responde `200 OK`, aunque el arreglo este vacio `[]`.
- Swagger muestra los endpoints del controlador de categorias.

Esta validacion cierra DEV: Config Server entrega configuracion y `catalogo-ms` mantiene su CRUD operativo. Recien despues de esto se pasa a PROD local.

Tambien puedes iniciar una segunda instancia en DEV desde otra terminal:

```bash
cd services/catalogo-ms
mvn spring-boot:run
```

Como `server.port` es dinamico (`0`), cada instancia toma un puerto libre. El comportamiento funcional debe mantenerse igual: ambas instancias leen la misma configuracion centralizada y responden el mismo CRUD.

### 3.11 Respetar el orden de arranque: infraestructura primero

**Producto del paso:** orden de ejecucion definido para que Config Server este disponible antes de levantar los microservicios.

En esta sesion no se crea la red de produccion manualmente. La infraestructura la prepara cuando se levanta con Docker Compose.

La regla de trabajo es:

```text
1. Levantar infraestructura
2. Levantar microservicios
```

En DEV:

```text
infra/config -> Config Server con Maven
services/catalogo-ms -> PostgreSQL DEV con Docker Compose + app con Maven
```

En PROD local:

```text
infra -> ecom-config con Docker Compose
services/catalogo-ms -> BD + catalogo-ms con Docker Compose
```

Este orden es importante porque los microservicios necesitan consultar Config Server al arrancar. En PROD local, `infra/compose.yml` crea la red compartida y luego `catalogo-ms` se conecta a esa red para resolver `http://ecom-config:8888`.

### 3.12 Dockerizar Config Server para PROD local

**Producto del paso:** Config Server preparado para ejecutarse como contenedor `ecom-config`.

En `infra/config/Dockerfile` se construye el JAR y se ejecuta con Java 17:

```dockerfile
FROM maven:3.9.9-eclipse-temurin-17 AS build
WORKDIR /app

COPY pom.xml .
RUN mvn -q -DskipTests dependency:go-offline

COPY src ./src
RUN mvn -q clean package -DskipTests

FROM eclipse-temurin:17-jre
WORKDIR /app

RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8888

ENTRYPOINT ["java", "-jar", "app.jar"]
```

En `infra/compose.yml`, Config Server se publica en el host como `28888` y monta `config-repo` dentro del contenedor:

```yaml
services:
  config:
    build:
      context: ./config
      dockerfile: Dockerfile
    container_name: ecom-config
    ports:
      - "28888:8888"
    volumes:
      - ./config/config-repo:/config-repo
    environment:
      SERVER_PORT: 8888
      SPRING_PROFILES_ACTIVE: native
      CONFIG_REPO_LOCATION: file:/config-repo
    networks:
      - ecom-prod-net
```

En PROD local, la ruta cambia porque ahora Config Server corre dentro de Docker:

```text
file:/config-repo
```

### 3.13 Probar Config Server en PROD local

**Producto del paso:** Config Server ejecutando como contenedor y entregando perfiles `prod`.

PowerShell / bash macOS/Linux:

```bash
cd infra
docker compose up -d --build config
docker compose ps
```

Consulta:

```bash
curl http://localhost:28888/catalogo-ms/prod
curl http://localhost:28888/actuator/health
curl http://localhost:28888/actuator/metrics
```

Resultado esperado:

- La respuesta de `catalogo-ms/prod` debe indicar `name: catalogo-ms`.
- La respuesta debe indicar `profiles: ["prod"]`.
- En `propertySources` debe aparecer `file:/config-repo/catalogo-ms-prod.yml`.
- Deben verse valores de PROD, por ejemplo `server.port: 8080`, `spring.flyway.enabled: true`, `spring.jpa.hibernate.ddl-auto: validate`, `springdoc.swagger-ui.enabled: false` y `springdoc.api-docs.enabled: false`.
- `/actuator/health` responde `UP`.
- `/actuator/metrics` responde la lista de metricas disponibles de Config Server.

### 3.14 Actualizar `catalogo-ms` para PROD local

**Producto del paso:** `catalogo-ms` preparado para consumir Config Server desde Docker.

En `.env` y `.env.example` de `catalogo-ms`, agrega o verifica:

```env
SPRING_PROFILES_ACTIVE=prod
CONFIG_SERVER_URL=http://ecom-config:8888

DB_NAME=ecom_catalogo_db
DB_USER=ecom
DB_PASS=ecom
```

En `compose.yml`, el microservicio debe recibir esas variables:

```yaml
environment:
  SPRING_PROFILES_ACTIVE: ${SPRING_PROFILES_ACTIVE}
  CONFIG_SERVER_URL: ${CONFIG_SERVER_URL}
  DB_HOST: ecom-postgres-catalogo
  DB_PORT: 5432
  DB_NAME: ${DB_NAME}
  DB_USER: ${DB_USER}
  DB_PASS: ${DB_PASS}
```

Y debe conectarse a la red compartida:

```yaml
networks:
  - ecom-catalogo-int
  - ecom-prod-net
```

### 3.15 Probar `catalogo-ms` en DEV y PROD local

**Producto del paso:** `catalogo-ms` verificado consumiendo configuracion centralizada en ambos ambientes.

DEV:

```bash
cd infra/config
mvn spring-boot:run
```

En otra terminal:

```bash
cd services/catalogo-ms
docker compose -f compose-dev.yml up -d
mvn spring-boot:run
```

PROD local:

```bash
cd infra
docker compose up -d --build config
```

En otra terminal:

```bash
cd services/catalogo-ms
docker compose up -d --build --scale catalogo-ms=2
```

Verifica health interno del MS:

```bash
docker run --rm --network ecom-catalogo-int curlimages/curl:8.10.1 -s http://catalogo-ms:8080/actuator/health
```

Verifica que el CRUD siga funcionando en PROD local:

```bash
docker run --rm --network ecom-catalogo-int curlimages/curl:8.10.1 -s http://catalogo-ms:8080/api/v1/categorias
```

Resultado esperado:

- `catalogo-ms` arranca con perfil `prod`.
- El microservicio obtiene su configuracion desde `http://ecom-config:8888`.
- `/actuator/health` responde `UP`.
- `/api/v1/categorias` responde `200 OK`, aunque el arreglo este vacio `[]`.
- Swagger no se prueba en PROD porque esta deshabilitado en `catalogo-ms-prod.yml`.
- La opcion `--scale catalogo-ms=2` levanta dos instancias del mismo microservicio. El cambio de S2 es interno: ahora ambas instancias leen configuracion desde Config Server.

Al terminar:

```bash
docker compose down
```

### 3.16 Repetir el patron con `producto-ms`

**Producto del paso:** `producto-ms` preparado para consumir configuracion centralizada.

Repite el mismo patron:

1. Crear `producto-ms-dev.yml`.
2. Crear `producto-ms-prod.yml`.
3. Dejar `application.yml` con `spring.application.name: producto-ms`.
4. Agregar `spring.config.import`.
5. Probar consulta HTTP:

```bash
curl http://localhost:18888/producto-ms/dev
curl http://localhost:18888/producto-ms/prod
```

### 3.17 Ruta alternativa: clonar y ejecutar a partir del tag final de la sesion

Esta seccion sirve si quieres partir del tag final de la sesion y solo levantar, probar y revisar evidencias sin repetir toda la construccion paso a paso.

PowerShell / bash macOS/Linux:

```bash
git clone --branch vs02-configuracion-centralizada https://github.com/261dist/ecom.git ecom-s02
cd ecom-s02
```

| Necesidad | Referencia |
|---|---|
| Levantar Config Server DEV | [Ver paso 3.6](#36-probar-config-server-en-dev) |
| Consultar perfiles por HTTP | [Ver paso 3.8](#38-consultar-perfiles-por-http) |
| Conectar `catalogo-ms` | [Ver paso 3.9](#39-conectar-catalogo-ms-como-config-client) |
| Probar Config Server PROD local | [Ver paso 3.13](#313-probar-config-server-en-prod-local) |
| Probar `catalogo-ms` DEV/PROD | [Ver paso 3.15](#315-probar-catalogo-ms-en-dev-y-prod-local) |

Comandos minimos DEV:

```bash
cd infra/config
mvn spring-boot:run
```

Comandos minimos PROD local:

```bash
cd infra
docker compose up -d --build config
docker compose ps
```

#### 3.17.1 Archivos clave

| Archivo | Proposito |
|---|---|
| `infra/config/pom.xml` | Dependencias del Config Server |
| `infra/config/src/main/resources/application.yml` | Configuracion del servidor |
| `infra/config/config-repo/*-dev.yml` | Configuracion DEV por servicio |
| `infra/config/config-repo/*-prod.yml` | Configuracion PROD por servicio |
| `infra/config/Dockerfile` | Imagen de Config Server |
| `infra/compose.yml` | Produccion local de infraestructura |
| `services/*/src/main/resources/application.yml` | Importacion de Config Server desde los microservicios |

## 4. Crea: actividad autonoma

Fuera del aula, cada estudiante consolida el aprendizaje aplicando configuracion externa a otro componente del sistema y entrega una evidencia individual.

Tiempo: 4h fuera del aula.

### 4.1 Plantilla de evidencia individual

Entrega un PDF con el siguiente nombre:

```text
S02_Equipo##_ApellidoNombre.pdf
```

Ejemplo:

```text
S02_Equipo03_QuispeAna.pdf
```

El PDF debe usar esta estructura. La primera seccion ya define el trabajo autonomo; completa las demas con tus evidencias.

#### 4.1.1 Datos del estudiante

- Nombre:
- Equipo:
- Sesion: S02 - Gestion centralizada de configuracion y ambientes
- Rol o aporte realizado:

#### 4.1.2 Trabajo autonomo realizado

Completa y evidencia estas tareas:

1. Completar la configuracion externa de `producto-ms`.
2. Comparar `catalogo-ms-dev.yml` con `catalogo-ms-prod.yml`.
3. Identificar un valor que no deberia quedar hardcodeado.
4. Consultar por HTTP al menos dos perfiles.
5. Verificar que el microservicio sigue funcionando.
6. Explicar como Config Server separa codigo y configuracion.

#### 4.1.3 Evidencia tecnica

Incluye capturas o salidas de consola con una breve explicacion debajo de cada una:

- Consulta en DEV `http://localhost:18888/producto-ms/dev`.
- Consulta en DEV del perfil PROD `http://localhost:18888/producto-ms/prod`.
- Prueba del microservicio funcionando en DEV.
- Prueba del microservicio funcionando en PROD local, si corresponde.
- Comparacion entre configuracion DEV y PROD.

No mezcles puertos en la evidencia DEV. Si Config Server esta corriendo con Maven, se consulta por `localhost:18888`, incluso cuando quieres revisar el perfil `prod`.

Usa `http://localhost:28888/producto-ms/prod` solo si ya levantaste Config Server en PROD local con Docker Compose desde `infra`.

#### 4.1.4 Error o hallazgo

Describe al menos un error, diferencia o hallazgo tecnico:

- Que ocurrio.
- Como lo diagnosticaste.
- Como lo corregiste o que aprendiste.

#### 4.1.5 Reflexion tecnica breve

Responde en 5 a 8 lineas:

```text
Como ayuda Config Server cuando el sistema crece a muchos microservicios e instancias?
```

### 4.2 Criterios minimos de aceptacion

La evidencia individual se considera completa si:

- El archivo respeta el nombre `S02_Equipo##_ApellidoNombre.pdf`.
- Incluye evidencias tecnicas legibles.
- Muestra configuracion externa de `producto-ms`.
- Compara al menos un valor entre DEV y PROD.
- Explica un aporte individual verificable.
- No contiene solo pantallazos: cada evidencia tiene una descripcion breve.

## 5. Cierre evaluativo

Tiempo: 20 min.

Esta seccion se revisa segun la programacion metodologica definida en la guia del curso. Conecta el resultado de aprendizaje con el producto que cada estudiante evidencio en la actividad autonoma.

La idea central de la sesion es que el sistema sigue funcionando igual para el usuario y para las pruebas, pero internamente queda preparado para administrar configuracion de muchos microservicios e instancias desde un punto central.

### 5.1 Resultados esperados

Al finalizar la sesion, el estudiante debe demostrar que:

- Config Server ejecuta en DEV.
- Config Server ejecuta en PROD local con Docker.
- `config-repo` entrega perfiles `dev` y `prod`.
- Un microservicio lee configuracion externa.
- Puede explicar la diferencia entre Config Server y Config repo.
- Puede diagnosticar un perfil no encontrado.

### 5.2 Evidencia del producto de sesion

Cada estudiante entrega un PDF individual siguiendo la plantilla de la seccion 4.1.

Nombre del archivo:

```text
S02_Equipo##_ApellidoNombre.pdf
```

La evidencia debe demostrar:

- Producto de sesion construido.
- Aporte individual verificable.
- Pruebas tecnicas realizadas.
- Reflexion tecnica breve.

La revision se realiza con los criterios minimos de aceptacion de la seccion 4.2 y la rubrica de la seccion 5.4.

### 5.3 Preguntas de defensa y reflexion

1. Que problema resuelve la configuracion centralizada?
2. Que diferencia hay entre Config Server y Config repo?
3. Por que `config-repo` puede estar dentro de `infra/config` y aun asi ser un componente logico separado?
4. Como se forma la URL `/{application}/{profile}`?
5. Que debe coincidir entre `spring.application.name` y los archivos de configuracion?
6. Que cambia entre DEV y PROD local?
7. Como diagnosticas un perfil no encontrado?

### 5.4 Rubrica de evaluacion

| Dimension | Peso | 3 - Logro destacado | 2 - Logro | 1 - Proceso | 0 - Inicio | Puntuacion obtenida |
|---|---:|---|---|---|---|---:|
| 1. Config Server operativo | 2 | Evidencia Config Server en DEV y PROD local, con health/metrics y perfiles correctos. | Evidencia Config Server en DEV con health/metrics y perfiles. | Evidencia parcial: arranca, pero sin health/metrics o perfiles claros. | No evidencia Config Server funcionando. | |
| 2. Configuracion externa DEV/PROD | 2 | Explica y evidencia `config-repo`, perfiles, diferencias DEV/PROD y valores no hardcodeados. | Muestra perfiles `dev` y `prod` con diferencias claras. | Muestra un perfil o configuracion incompleta. | No evidencia separacion entre codigo y configuracion. | |
| 3. Microservicio como Config Client | 2 | Evidencia Config Client, health, metrics y CRUD funcionando despues de externalizar configuracion. | Evidencia que el microservicio arranca leyendo Config Server y responde health o CRUD. | Evidencia arranque parcial o sin prueba funcional. | No demuestra conexion del microservicio con Config Server. | |
| 4. Aporte individual verificable | 2 | Aporte claro, verificable y conectado al producto del equipo. | Aporte claro con archivo, comando o prueba realizada. | Aporte mencionado de forma general. | No se identifica aporte individual. | |
| 5. Diagnostico de error o hallazgo | 1 | Analiza error/hallazgo, causa, solucion y aprendizaje tecnico. | Explica causa probable y solucion parcial. | Menciona un problema sin explicarlo. | No presenta error ni hallazgo. | |
| 6. Reflexion tecnica y orden | 1 | Reflexion tecnica precisa, PDF ordenado, capturas legibles y explicaciones breves. | Reflexion clara y evidencias entendibles. | Reflexion superficial o evidencias poco legibles. | PDF desordenado o sin reflexion. | |

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
