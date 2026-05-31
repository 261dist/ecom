# S1 - Construccion de un servicio base para un sistema distribuido

## 1. Introduccion

### 1.1 Proposito

Construir el primer servicio de negocio del sistema y dejarlo preparado para crecer hacia una arquitectura distribuida.

### 1.2 Resultado de aprendizaje

El estudiante implementa un microservicio stateless con API REST, persistencia, validacion, documentacion de endpoints, health check y ejecucion reproducible en desarrollo y produccion.

### 1.3 Producto de sesion

`catalogo-ms` funcional con CRUD de categorias, PostgreSQL en Docker, Swagger, Actuator, README operativo y pruebas por shell.

### 1.4 Motivacion de la sesion

#### 1.4.1 Caso: plataforma de comercio electronico

Una empresa desarrolla un sistema de comercio electronico. Inicialmente, todo el sistema fue construido como una sola aplicacion monolitica.

Con el crecimiento del negocio comienzan a aparecer problemas:

- El sistema tarda mas en desplegarse.
- Errores en un modulo afectan a todo el sistema.
- Es dificil escalar partes especificas del sistema.
- Los equipos de desarrollo trabajan sobre el mismo codigo.

El equipo de ingenieria decide redisenar la arquitectura del sistema utilizando microservicios.

Preguntas para los estudiantes:

1. Que problemas tiene la arquitectura monolitica en este caso?
2. Por que una empresa migraria a microservicios?
3. Que ventajas ofrece dividir el sistema en servicios?

En esta sesion se inicia ese redisenio construyendo el primer componente del sistema ecom: `catalogo-ms`.

### 1.5 Ubicacion en el curso

- Unidad: U1 - Sistema distribuido base orientado a produccion.
- Producto de unidad: sistema distribuido base funcional, configurable y preparado para multiples instancias, ejecutable en desarrollo y produccion local en paralelo.
- Avance del producto en esta sesion: primer microservicio REST funcional, persistente, observable y ejecutable fuera del IDE.

Roadmap para elaborar el producto de la unidad:

```mermaid
flowchart LR
    Cliente["Cliente de prueba<br/>PowerShell / bash / Swagger"]
    Gateway["Gateway<br/>punto unico de acceso<br/>balanceo de carga"]
    Eureka["Registro de servicios<br/>Eureka"]
    Config["Servidor de configuracion<br/>Config Server"]
    Repo["Repositorio de configuracion<br/>catalogo-ms.yml<br/>producto-ms.yml"]
    Catalogo["catalogo-ms<br/>HOY<br/>REST + BD + health"]
    Producto["producto-ms<br/>trabajo aplicado"]

    Cliente --> Gateway
    Gateway --> Catalogo
    Gateway --> Producto
    Gateway -. descubre servicios .-> Eureka
    Catalogo -. registra instancia .-> Eureka
    Producto -. registra instancia .-> Eureka
    Catalogo -. carga configuracion .-> Config
    Producto -. carga configuracion .-> Config
    Config --> Repo

    classDef today fill:#ffe08a,stroke:#9a6b00,stroke-width:2px,color:#111;
    class Catalogo today;
```

Hoy se construye el primer componente real de la U1: `catalogo-ms`. En las siguientes sesiones se agregan configuracion centralizada, registro de servicios, multiples instancias, Gateway y balanceo. La evaluacion U1 valida el sistema base integrado construido con esos componentes.

## 2. Explica

### 2.1 Conceptos clave

Un microservicio debe tener responsabilidad clara, persistencia propia, configuracion por ambiente y capacidad de ejecutarse de forma independiente.

Ejemplo: `catalogo-ms` se encarga de gestionar categorias y su propia base de datos. No deberia guardar productos, ordenes ni pagos. Si mas adelante `producto-ms` necesita saber a que categoria pertenece un producto, consulta a `catalogo-ms` por red en lugar de leer directamente su base de datos.

### 2.2 Arquitectura del producto en `ecom`

#### 2.2.1 DEV: aplicacion fuera de Docker

```mermaid
flowchart TB
    DevClient["Cliente<br/>PowerShell / bash / Swagger"]
    DevApp1["catalogo-ms<br/>Java 17 + Maven<br/>puerto dinamico"]
    DevApp2["catalogo-ms<br/>segunda instancia<br/>puerto dinamico"]
    subgraph DevDocker["Docker: solo base de datos"]
        DevDb[("ecom_catalogo_db<br/>PostgreSQL<br/>localhost:15432 -> 5432")]
    end

    DevClient -->|"localhost:<puerto-asignado>"| DevApp1
    DevClient -->|"localhost:<otro-puerto>"| DevApp2
    DevApp1 -->|"localhost:15432"| DevDb
    DevApp2 -->|"localhost:15432"| DevDb

    classDef app fill:#eef6ff,stroke:#2b6cb0,color:#111;
    classDef db fill:#fff4de,stroke:#b7791f,color:#111;
    class DevApp1,DevApp2 app;
    class DevDb db;
```

#### 2.2.2 PROD local: aplicacion dentro de Docker

```mermaid
flowchart TB
    ProdClient["Cliente interno<br/>curl container"]
    subgraph ProdDocker["Docker Network: ecom-catalogo-int"]
        ProdApp1["catalogo-ms<br/>jar<br/>8080 interno"]
        ProdApp2["catalogo-ms<br/>jar<br/>8080 interno"]
        ProdDb[("ecom_catalogo_db<br/>PostgreSQL<br/>ecom-postgres-catalogo:5432")]
    end

    ProdClient -->|"catalogo-ms:8080"| ProdApp1
    ProdClient -->|"catalogo-ms:8080"| ProdApp2
    ProdApp1 -->|"ecom-postgres-catalogo:5432"| ProdDb
    ProdApp2 -->|"ecom-postgres-catalogo:5432"| ProdDb

    classDef app fill:#eef6ff,stroke:#2b6cb0,color:#111;
    classDef db fill:#fff4de,stroke:#b7791f,color:#111;
    class ProdApp1,ProdApp2 app;
    class ProdDb db;
```

Regla practica:

- Si la aplicacion corre fuera de Docker, usa `localhost` con el puerto expuesto por Docker.
- Si la aplicacion corre dentro de Docker, usa el nombre del servicio y el puerto interno.

#### 2.2.3 Flujo de trabajo

1. Preparar ambiente.
2. Crear proyecto Spring Boot y levantar PostgreSQL DEV.
3. Construir el CRUD de `Categoria`.
4. Ejecutar y probar en DEV.
5. Preparar archivos de PROD local.
6. Ejecutar y probar en Docker.
7. Registrar evidencias y defender el resultado.

### 2.3 Observabilidad y diagnostico

La observabilidad inicia desde S1 como habito transversal. En esta sesion todavia no hay stack completo de metricas y paneles, pero el estudiante ya debe revisar senales basicas del servicio y usar los errores como insumo de diagnostico.

#### 2.3.1 Senales basicas a revisar

- Logs de arranque.
- Puerto dinamico asignado.
- Estado de `/actuator/health`.
- Metricas de `/actuator/metrics`.
- Conexion a PostgreSQL.
- Migraciones Flyway ejecutadas.
- Errores de validacion HTTP 400.
- Logs de contenedores con `docker compose logs`.

#### 2.3.2 Errores frecuentes y diagnostico

| Problema | Causa probable | Solucion |
|---|---|---|
| No conecta a BD | PostgreSQL apagado o puerto incorrecto | Revisar compose y variables |
| Swagger no abre | Puerto dinamico no identificado | Revisar consola o Eureka cuando aplique |
| Validacion no responde | Falta `@Valid` o anotaciones | Revisar controlador y DTO |
| PROD local no responde desde host | El microservicio no publica puerto host | Probar desde red Docker o esperar Gateway |
| Escalado consume demasiados recursos | Muchas instancias locales | Usar maximo dos instancias |

## 3. Aplica: actividad practica guiada

En el laboratorio, el docente guia la construccion de `catalogo-ms` y los estudiantes verifican el resultado con comandos de consola.

Duracion: 4h.

En `ecom`, el docente guia `catalogo-ms` y el estudiante replica el patron en `producto-ms` como trabajo aplicado. La version actual usa monorepo, nombres con sufijo `-ms`, PostgreSQL y puertos dinamicos para los microservicios.

- Crear o revisar el microservicio base.
- Implementar entidad, repositorio, servicio y controlador.
- Levantar PostgreSQL DEV y probar endpoints.
- Revisar Swagger, health y README.
- Cerrar con una ejecucion breve en produccion local con Docker.

### 3.1 Preparar ambiente local: Java 17, Maven, Docker y VS Code

**Producto del paso:** ambiente local con Java 17, Maven, Docker, Docker Compose y VS Code verificados, listo para crear y ejecutar el microservicio.

Antes de crear el microservicio, el estudiante debe preparar el entorno DEV. En esta sesion Java y Maven se ejecutan en el host; PostgreSQL no se instala en el host, se levanta con Docker desde el paso 3.2.

**Herramientas necesarias**

- Java 17.
- Maven 3.x.
- Docker Desktop.
- VS Code.
- Extension Pack for Java.
- Spring Boot Extension Pack.

Puedes usar otro IDE si ya lo dominas, pero en este curso se trabajara con VS Code para mantener una guia comun. Aun usando IDE, la ejecucion recomendada del microservicio sera desde la consola de comandos, al estilo de un servidor Linux.

#### 3.1.1 Instalar gestor de paquetes en Windows o macOS, si no existe

Si trabajas en Windows y no tienes Chocolatey, abre PowerShell como administrador y ejecuta:

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Luego cierra y vuelve a abrir PowerShell.

Si no vas a usar Chocolatey para instalar Java en Windows, tambien puedes descargar Java 17 directamente desde https://adoptium.net.

Si trabajas en macOS y no tienes Homebrew, abre Terminal y ejecuta:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Luego cierra y vuelve a abrir Terminal.

#### 3.1.2 Instalar o verificar Java 17

En Windows con Chocolatey:

```powershell
choco install temurin17 -y
```

En macOS con Homebrew:

```bash
brew install --cask temurin@17
```

En Linux Debian/Ubuntu:

```bash
sudo apt update
sudo apt install -y openjdk-17-jdk
```

Verificar instalacion:

PowerShell / bash macOS/Linux:

```bash
java -version
```

Resultado esperado:

```text
version 17
```

#### 3.1.3 Instalar o verificar Maven 3.x

En Windows con Chocolatey:

```powershell
choco install maven -y
```

En macOS con Homebrew:

```bash
brew install maven
```

En Linux Debian/Ubuntu:

```bash
sudo apt update
sudo apt install -y maven
```

Verificar instalacion:

PowerShell / bash macOS/Linux:

```bash
mvn -version
```

Resultado esperado:

```text
Apache Maven
Java version: 17
```

Uso esperado de Maven: ubicarse en la carpeta donde esta el `pom.xml` del microservicio y ejecutar:

```bash
mvn spring-boot:run
```

#### 3.1.4 Instalar o verificar Docker Desktop y Docker Compose

Opcional recomendado: antes de iniciar el laboratorio, crea una cuenta gratuita en Docker Hub:

```text
https://hub.docker.com/signup
```

Docker funciona sin iniciar sesion, pero Docker Hub puede aplicar limites de descarga de imagenes. En equipos de laboratorio o redes compartidas, iniciar sesion ayuda a evitar bloqueos durante la descarga de imagenes como PostgreSQL.

PowerShell / bash macOS/Linux:

```bash
docker login
```

En Windows, Docker Compose se instala junto con Docker Desktop:

```text
https://www.docker.com/products/docker-desktop
```

En macOS, Docker Compose tambien viene incluido con Docker Desktop:

```text
https://www.docker.com/products/docker-desktop
```

En Linux puedes usar Docker Engine con el plugin Compose siguiendo la documentacion oficial de Docker:

```text
https://docs.docker.com/engine/install/
https://docs.docker.com/compose/install/linux/
```

Verificar Docker:

PowerShell / bash macOS/Linux:

```bash
docker version
docker compose version
docker ps
```

Resultado esperado:

```text
Docker version
Docker Compose version
```

#### 3.1.5 Abrir el proyecto en VS Code

Ubicate en la raiz del monorepo `ecom`, no dentro de un microservicio especifico. VS Code soporta trabajar con multiples proyectos/carpetas dentro del mismo workspace; abrir la raiz evita tener una ventana distinta por cada microservicio.

PowerShell / bash macOS/Linux:

```bash
cd c:/262/262dist/pagatu/ms1/ecom
code .
```

Desde VS Code, confirmar que se reconoce el proyecto Java y que las extensiones de Spring Boot estan disponibles.

**Evidencia de cierre del paso 3.1**

- Salida de `java -version`.
- Salida de `mvn -version`.
- Salida de `docker version`.
- Salida de `docker compose version`.
- VS Code abierto en la raiz del repositorio `ecom`.

### 3.2 Crear el proyecto Spring Boot desde VS Code con dependencias base

**Producto del paso:** proyecto Spring Boot creado en `services/catalogo-ms`, con `artifactId` `ecom-catalogo-ms`, paquete `com.upeu.catalogo`, dependencias base instaladas, PostgreSQL DEV levantado en Docker y un endpoint web simple respondiendo desde el navegador o shell.

En este paso no basta con crear el proyecto. Como se agregan `Spring Data JPA`, `PostgreSQL Driver` y `Flyway`, Spring Boot intentara configurar una conexion a base de datos al arrancar. Por eso, si ejecutas el microservicio sin configurar y levantar PostgreSQL, el arranque fallara.

Ese fallo es util para aprender: un microservicio con persistencia necesita una dependencia de infraestructura disponible. En el curso no usaremos H2 para ocultar el problema ni desactivaremos la conexion a BD; levantaremos PostgreSQL con Docker desde el inicio.

#### 3.2.1 Crear el proyecto con Spring Initializr desde VS Code

Desde la raiz del monorepo `ecom`, abre VS Code y ejecuta el comando:

```text
Spring Initializr: Create a Maven Project
```

Usa la siguiente configuracion:

| Campo | Valor |
|---|---|
| Project | Maven Project |
| Spring Boot | 3.5.x |
| Language | Java |
| Java | 17 |
| Group Id | `com.upeu` |
| Artifact Id | `ecom-catalogo-ms` |
| Package name | `com.upeu.catalogo` |
| Packaging | Jar |
| Ubicacion | `services/catalogo-ms` |

Dependencias a seleccionar:

| Grupo | Dependencias | Proposito |
|---|---|---|
| API REST base | Spring Web, Validation | Exponer endpoints HTTP y validar entradas |
| Productividad | Lombok, Spring Boot DevTools | Reducir codigo repetitivo y facilitar ejecucion en desarrollo |
| Documentacion y operacion | SpringDoc OpenAPI WebMvc UI, Spring Boot Actuator | Documentar la API con Swagger y verificar health |
| Persistencia | Spring Data JPA, PostgreSQL Driver, Flyway | Acceso a datos, conexion a PostgreSQL y migraciones de BD |

Nota: SpringDoc/Swagger documenta los endpoints del microservicio; no es infraestructura distribuida. La infraestructura distribuida inicia desde S2 con configuracion centralizada.

Nota: el directorio del microservicio en el monorepo es `services/catalogo-ms`, pero el `artifactId` Maven usado por el proyecto actual es `ecom-catalogo-ms`.

#### 3.2.2 Revisar dependencias PostgreSQL y Flyway

Abre `services/catalogo-ms/pom.xml` y verifica que existan las dependencias de persistencia para PostgreSQL:

```xml
<dependency>
    <groupId>org.flywaydb</groupId>
    <artifactId>flyway-core</artifactId>
</dependency>
<dependency>
    <groupId>org.flywaydb</groupId>
    <artifactId>flyway-database-postgresql</artifactId>
</dependency>
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <scope>runtime</scope>
</dependency>
```

Si vienes de material anterior con MySQL, reemplaza la idea de `flyway-mysql` y `mysql-connector` por PostgreSQL.

#### 3.2.3 Ejecutar una primera vez y reconocer el fallo esperado

Ubicate en la carpeta del microservicio:

PowerShell / bash macOS/Linux:

```bash
cd services/catalogo-ms
mvn spring-boot:run
```

Si todavia no existe configuracion de base de datos, el error esperado sera parecido a:

```text
APPLICATION FAILED TO START
Failed to configure a DataSource: 'url' attribute is not specified and no embedded datasource could be configured.
Reason: Failed to determine a suitable driver class
```

No se corrige quitando JPA ni usando H2. Se corrige declarando PostgreSQL DEV y levantando la base de datos con Docker.

#### 3.2.4 Crear `compose-dev.yml` para PostgreSQL DEV

En `services/catalogo-ms`, crea el archivo `compose-dev.yml`:

```yaml
name: ecom-catalogo-dev

services:
  postgres-catalogo-dev:
    image: postgres:16-alpine
    container_name: ecom-postgres-catalogo-dev
    restart: unless-stopped
    environment:
      POSTGRES_DB: ecom_catalogo_db
      POSTGRES_USER: ecom
      POSTGRES_PASSWORD: ecom
    ports:
      - "15432:5432"
    volumes:
      - ecom_catalogo_dev_data:/var/lib/postgresql/data

volumes:
  ecom_catalogo_dev_data:
```

Levanta la base de datos:

PowerShell / bash macOS/Linux:

```bash
docker compose -f compose-dev.yml up -d
docker ps
```

#### 3.2.5 Configurar `application.yml` y `application-dev.yml`

En S1 la aplicacion `catalogo-ms` se ejecuta en DEV con Maven desde el host. Solo PostgreSQL se ejecuta en Docker. Por eso la configuracion debe apuntar a `localhost:15432`, que es el puerto publicado por el contenedor de base de datos.

En `src/main/resources`, crea o ajusta `application.yml` como configuracion base:

```yaml
spring:
  application:
    name: catalogo-ms
  profiles:
    active: dev
```

Luego crea `application-dev.yml` para la configuracion de desarrollo:

```yaml
server:
  port: 0

spring:
  datasource:
    url: jdbc:postgresql://localhost:15432/ecom_catalogo_db
    username: ecom
    password: ecom
  jpa:
    hibernate:
      ddl-auto: validate
    show-sql: true
    properties:
      hibernate:
        format_sql: true
  flyway:
    enabled: true

management:
  endpoints:
    web:
      exposure:
        include: health,info
  endpoint:
    health:
      show-details: always
```

Con `server.port: 0`, Spring Boot asigna un puerto libre automaticamente. Esto permite levantar varias instancias del mismo microservicio en paralelo sin cambiar el archivo de configuracion.

En S2 esta configuracion se movera progresivamente al Config Server. En S1 se mantiene local para que el alumno entienda primero que necesita el microservicio para arrancar.

#### 3.2.6 Crear un endpoint temporal de saludo

Antes del CRUD, crea un controlador minimo para comprobar que la aplicacion web responde.

Archivo: `src/main/java/com/upeu/catalogo/controller/SaludoController.java`

```java
package com.upeu.catalogo.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class SaludoController {

    @GetMapping("/saludo")
    public String saludo() {
        return "catalogo-ms activo";
    }
}
```

Este endpoint es temporal para validar el arranque web. Luego el foco pasara al CRUD de categorias.

#### 3.2.7 Ejecutar y comprobar que ya no falla

Antes de ejecutar la aplicacion, comprueba desde la consola que PostgreSQL DEV esta listo y que la base de datos existe.

PowerShell / bash macOS/Linux:

```bash
docker exec -it ecom-postgres-catalogo-dev psql -U ecom -d ecom_catalogo_db -c "SELECT current_database();"
docker exec -it ecom-postgres-catalogo-dev psql -U ecom -d ecom_catalogo_db -c "\dt"
```

Resultado esperado:

```text
current_database
------------------
ecom_catalogo_db
```

Si `\dt` muestra `Did not find any relations`, esta bien en este momento: aun no se ha creado la tabla `categorias`.

Con PostgreSQL DEV levantado y verificado, ejecuta la aplicacion:

PowerShell / bash macOS/Linux:

```bash
mvn spring-boot:run
```

Prueba el endpoint:

PowerShell:

```powershell
Invoke-RestMethod `
  -Method Get `
  -Uri "http://localhost:<puerto-asignado>/saludo"
```

bash macOS/Linux:

```bash
curl http://localhost:<puerto-asignado>/saludo
```

Resultado esperado:

```text
catalogo-ms activo
```

Tambien puedes revisar Swagger usando el puerto que aparezca en la consola de arranque:

```text
http://localhost:<puerto-asignado>/swagger-ui/index.html
```

**Evidencia de cierre del paso 3.2**

- Proyecto creado en `services/catalogo-ms`.
- `pom.xml` con dependencias base y persistencia PostgreSQL.
- PostgreSQL DEV ejecutando en Docker.
- `application.yml` con perfil `dev` activo.
- `application-dev.yml` con puerto dinamico y conexion a PostgreSQL DEV.
- Endpoint `/saludo` respondiendo.

### 3.3 Construir el CRUD de `Categoria` con una base de apoyo

**Producto del paso:** CRUD de `Categoria` incorporado en `catalogo-ms`, incluyendo entidad, capas de aplicacion, validaciones y migracion de base de datos.

En esta sesion se trabajara con la entidad `Categoria` como primer recurso del microservicio `catalogo-ms`. La entidad representa la tabla `categorias` y sera la base para construir el CRUD.

#### 3.3.1 Revisar la entidad principal

Entidad de referencia:

```java
@Entity
@Table(name = "categorias")
@Getter
@Setter
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class Categoria {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "nombre", nullable = false, length = 100)
    private String nombre;

    @Column(name = "descripcion", length = 255)
    private String descripcion;
}
```

Para avanzar sin consumir demasiado tiempo escribiendo codigo repetitivo, se usara una repo base ya preparada. Desde una carpeta temporal fuera del monorepo principal, clona la version base:

#### 3.3.2 Clonar la repo base

PowerShell / bash macOS/Linux:

```bash
git clone --branch vs01-arquitectura-base https://github.com/261dist/catalogo.git
```

#### 3.3.3 Copiar carpetas del CRUD

Copia desde la repo base hacia `services/catalogo-ms/src/main/java/com/upeu/catalogo` las carpetas del CRUD. Si ya existen, reemplazalas:

```text
config
controller
dto
entity
exception
filter
mapper
repository
service
```

Copia tambien la carpeta de migraciones:

```text
src/main/resources/db
```

No copies `CatalogoApplication.java` si ya existe en tu proyecto. Ese archivo es la clase principal de arranque y debe quedar una sola version.

#### 3.3.4 Revisar estructura resultante

Despues de copiar, revisa que la estructura de `catalogo-ms` quede similar a:

```text
src/main/java/com/upeu/catalogo
  config/
  controller/
  dto/
  entity/
  exception/
  filter/
  mapper/
  repository/
  service/
  CatalogoApplication.java
src/main/resources/db/migration
  V1__create_categorias_table.sql
```

#### 3.3.5 Revisar cada capa

Revisa cada carpeta copiada antes de ejecutar:

```text
entity      -> modelo persistente Categoria
repository  -> acceso a datos con JPA
service     -> logica de aplicacion
controller  -> endpoints REST
dto         -> datos de entrada y salida
mapper      -> conversion entre entidad y DTO
exception   -> manejo de errores
filter      -> filtros HTTP cuando aplique
config      -> configuraciones locales del servicio
```

#### 3.3.6 Revisar validaciones

Verifica que los DTOs tengan anotaciones de validacion y que el controlador use `@Valid` en los metodos que reciben `@RequestBody`:

```java
@NotBlank
@Size(max = 100)
private String nombre;
```

La validacion evita que el microservicio acepte datos incompletos antes de llegar a la base de datos.

#### 3.3.7 Revisar migracion Flyway

Revisa tambien la migracion copiada en `src/main/resources/db/migration`:

```text
V1__create_categorias_table.sql
```

Contenido esperado:

```sql
CREATE TABLE IF NOT EXISTS categorias (
    id BIGINT GENERATED BY DEFAULT AS IDENTITY,
    nombre VARCHAR(100) NOT NULL,
    descripcion VARCHAR(255),
    PRIMARY KEY (id)
);
```

Como `application-dev.yml` usa `spring.jpa.hibernate.ddl-auto: validate`, Hibernate no crea la tabla automaticamente. Flyway debe crearla primero y luego Hibernate valida que la entidad coincida con la base de datos.

#### 3.3.8 Preguntas de verificacion antes de ejecutar

Antes de ejecutar, la lectura del CRUD debe responder:

1. Que clase representa la tabla `categorias`?
2. Que archivo recibe la peticion HTTP?
3. Que archivo concentra la logica de aplicacion?
4. Que archivo conversa con JPA?
5. Que DTO se usa para recibir datos desde la API?
6. Que excepcion se devuelve cuando no existe una categoria?

### 3.4 Ejecutar y probar el microservicio en DEV

**Producto del paso:** microservicio ejecutando en desarrollo fuera del IDE, tabla `categorias` creada por Flyway, Swagger disponible, health activo y CRUD verificado por shell.

#### 3.4.1 Verificar PostgreSQL DEV

Verifica que PostgreSQL DEV siga activo:

PowerShell / bash macOS/Linux:

```bash
docker ps
```

#### 3.4.2 Ejecutar con Maven

Ejecuta el microservicio:

PowerShell / bash macOS/Linux:

```bash
cd services/catalogo-ms
mvn spring-boot:run
```

En la consola identifica el puerto asignado por Spring Boot. Debes ver una linea similar a:

```text
Tomcat started on port XXXXX
```

#### 3.4.3 Verificar tabla creada por Flyway

Luego verifica que Flyway haya creado la tabla:

PowerShell / bash macOS/Linux:

```bash
docker exec -it ecom-postgres-catalogo-dev psql -U ecom -d ecom_catalogo_db -c "\dt"
docker exec -it ecom-postgres-catalogo-dev psql -U ecom -d ecom_catalogo_db -c "\d categorias"
```

#### 3.4.4 Revisar Swagger

Abre Swagger usando el puerto que aparece en la consola:

```text
http://localhost:<puerto-asignado>/swagger-ui/index.html
```

Verifica que aparezcan las operaciones del controlador de categorias.

#### 3.4.5 Verificar health y metrics

Verifica `/actuator/health`:

PowerShell:

```powershell
Invoke-RestMethod `
  -Method Get `
  -Uri "http://localhost:<puerto-asignado>/actuator/health"
```

bash macOS/Linux:

```bash
curl http://localhost:<puerto-asignado>/actuator/health
```

Verifica `/actuator/metrics`. Este endpoint solo requiere `spring-boot-starter-actuator`; no necesita una libreria adicional.

PowerShell:

```powershell
Invoke-RestMethod `
  -Method Get `
  -Uri "http://localhost:<puerto-asignado>/actuator/metrics"
```

bash macOS/Linux:

```bash
curl http://localhost:<puerto-asignado>/actuator/metrics
```

Tambien puedes consultar una metrica especifica:

```bash
curl http://localhost:<puerto-asignado>/actuator/metrics/jvm.memory.used
```

Nota: para exponer `/actuator/prometheus` si se requiere `micrometer-registry-prometheus`.

#### 3.4.6 Probar CRUD por shell

Prueba el CRUD de categorias por shell.

Pendiente de desarrollo.

#### 3.4.7 Ejecutar una segunda instancia en DEV

Para cerrar el paso, ejecuta una segunda instancia del microservicio en otra terminal. Como `application-dev.yml` usa `server.port: 0`, Spring Boot asignara otro puerto libre automaticamente.

PowerShell / bash macOS/Linux:

```bash
cd services/catalogo-ms
mvn spring-boot:run
```

Verifica en cada terminal que los puertos sean diferentes. Esta prueba demuestra que el microservicio puede ejecutarse en multiples instancias en DEV sin cambiar la configuracion.

### 3.5 Configurar produccion local con Docker

**Producto del paso:** archivos de produccion local preparados: `Dockerfile`, `.env`, `.env.example`, `compose.yml` y `application-prod.yml`.

En DEV la aplicacion se ejecuta con Maven desde el host y solo PostgreSQL corre en Docker. En PROD local, la aplicacion tambien se ejecutara como contenedor. Por eso se agregan archivos separados para construir la imagen, pasar variables de entorno y conectar el contenedor de la aplicacion con su PostgreSQL dockerizado.

Agrega o revisa estos archivos en `services/catalogo-ms`:

```text
.env
.env.example
Dockerfile
compose.yml
```

Y este archivo en `services/catalogo-ms/src/main/resources`:

```text
application-prod.yml
```

#### 3.5.1 Crear `Dockerfile`

El `Dockerfile` construye el JAR con Maven y luego ejecuta la aplicacion con Java 17:

```dockerfile
FROM maven:3.9.9-eclipse-temurin-17 AS build
WORKDIR /app

COPY pom.xml .
RUN mvn -q -DskipTests dependency:go-offline

COPY src ./src
RUN mvn -q clean package -DskipTests

FROM eclipse-temurin:17-jre
WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
```

#### 3.5.2 Crear `.env` y `.env.example`

`.env` contiene variables para produccion local. `.env.example` debe tener la misma estructura para que otro estudiante pueda reproducir el entorno sin adivinar nombres.

```env
SPRING_PROFILES_ACTIVE=prod

DB_NAME=ecom_catalogo_db
DB_USER=ecom
DB_PASS=ecom
```

En S2 se agregara la URL del Config Server. En S1 el objetivo es que el microservicio pueda ejecutar en produccion local con configuracion propia.

#### 3.5.3 Crear `application-prod.yml`

`application-prod.yml` define como se comporta la aplicacion dentro de Docker. La base de datos no se busca en `localhost`, sino por el nombre del servicio PostgreSQL declarado en `compose.yml`.

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

#### 3.5.4 Crear `compose.yml`

`compose.yml` levanta PostgreSQL y el microservicio en contenedores. La base de datos queda en una red interna del microservicio y la aplicacion queda preparada para conectarse despues a una red compartida del sistema.

```yaml
name: ecom-catalogo-prod

services:
  postgres-catalogo:
    image: postgres:16-alpine
    container_name: ecom-postgres-catalogo
    restart: unless-stopped
    environment:
      POSTGRES_DB: ${DB_NAME}
      POSTGRES_USER: ${DB_USER}
      POSTGRES_PASSWORD: ${DB_PASS}
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ${DB_USER} -d ${DB_NAME}"]
      interval: 10s
      timeout: 5s
      retries: 10
      start_period: 20s
    volumes:
      - ecom_catalogo_data:/var/lib/postgresql/data
    ports:
      - "25432:5432"
    networks:
      - ecom-catalogo-int

  catalogo-ms:
    build: .
    restart: unless-stopped
    depends_on:
      postgres-catalogo:
        condition: service_healthy
    environment:
      SPRING_PROFILES_ACTIVE: ${SPRING_PROFILES_ACTIVE}
      DB_HOST: ecom-postgres-catalogo
      DB_PORT: 5432
      DB_NAME: ${DB_NAME}
      DB_USER: ${DB_USER}
      DB_PASS: ${DB_PASS}
    volumes:
      - ./logs:/app/logs
    networks:
      - ecom-catalogo-int

volumes:
  ecom_catalogo_data:

networks:
  ecom-catalogo-int:
    name: ecom-catalogo-int
```

En S1 basta con la red interna del microservicio. Mas adelante, cuando aparezcan Gateway, Eureka y Config Server, la aplicacion se conectara tambien a la red compartida del sistema.

### 3.6 Probar produccion local con Docker

**Producto del paso:** microservicio ejecutando en produccion local con Docker, PostgreSQL PROD disponible y escalado controlado a dos instancias.

#### 3.6.1 Levantar produccion local

PowerShell / bash macOS/Linux:

```bash
cd services/catalogo-ms
docker compose up -d --build --scale catalogo-ms=2
docker compose ps
```

#### 3.6.2 Verificar la base de datos PROD

PowerShell / bash macOS/Linux:

```bash
docker exec -it ecom-postgres-catalogo psql -U ecom -d ecom_catalogo_db -c "\dt"
docker exec -it ecom-postgres-catalogo psql -U ecom -d ecom_catalogo_db -c "\d categorias"
```

#### 3.6.3 Verificar health desde la red Docker

En S1 el microservicio en PROD local no publica puerto host directo. Se valida desde la red Docker interna; en sesiones posteriores el acceso externo se hara por Gateway.

PowerShell / bash macOS/Linux:

```bash
docker run --rm --network ecom-catalogo-int curlimages/curl:8.10.1 -s http://catalogo-ms:8080/actuator/health
```

Resultado esperado:

```json
{"status":"UP"}
```

#### 3.6.4 Revisar logs y bajar el entorno

La produccion local se levanto con dos instancias usando `--scale catalogo-ms=2`. No uses mas de dos en laboratorio porque cada instancia consume CPU y memoria.

PowerShell / bash macOS/Linux:

```bash
docker compose ps
```

Revisa logs de ambas instancias:

```bash
docker compose logs --tail=80 catalogo-ms
```

Al terminar la evidencia, baja el entorno para liberar CPU, memoria, red y contenedores:

```bash
docker compose down
```

### 3.7 Ruta alternativa: clonar y ejecutar a partir del tag final de la sesion

Esta seccion sirve si quieres partir del tag final de la sesion y solo levantar, probar y revisar evidencias sin repetir toda la construccion paso a paso.

| Necesidad | Referencia |
|---|---|
| Levantar y probar en DEV | [Ver paso 3.4](#34-ejecutar-y-probar-el-microservicio-en-dev) |
| Revisar Swagger | [Ver paso 3.4.4](#344-revisar-swagger) |
| Revisar health y metrics | [Ver paso 3.4.5](#345-verificar-health-y-metrics) |
| Probar CRUD por shell | [Ver paso 3.4.6](#346-probar-crud-por-shell) |
| Levantar y escalar PROD local | [Ver paso 3.6](#36-probar-produccion-local-con-docker) |

Comandos minimos DEV:

PowerShell / bash macOS/Linux:

```bash
cd services/catalogo-ms
docker compose -f compose-dev.yml up -d
mvn spring-boot:run
```

Comandos minimos PROD local:

```bash
cd services/catalogo-ms
docker compose up -d --build --scale catalogo-ms=2
docker compose ps
```

### 3.7.1 Archivos clave por modo de ejecucion

DEV:

| Archivo | Proposito |
|---|---|
| `services/catalogo-ms/compose-dev.yml` | PostgreSQL DEV |
| `services/catalogo-ms/src/main/resources/application.yml` | Configuracion base y perfil activo |
| `services/catalogo-ms/src/main/resources/application-dev.yml` | Configuracion DEV con puerto dinamico y BD DEV |

PROD local:

| Archivo | Proposito |
|---|---|
| `services/catalogo-ms/Dockerfile` | Imagen de aplicacion |
| `services/catalogo-ms/compose.yml` | Produccion local con Docker |
| `services/catalogo-ms/.env.example` | Variables esperadas para PROD local |
| `services/catalogo-ms/.env` | Variables locales de ejecucion PROD |
| `services/catalogo-ms/src/main/resources/application-prod.yml` | Configuracion PROD local |

Comunes:

| Archivo | Proposito |
|---|---|
| `services/catalogo-ms/pom.xml` | Dependencias del microservicio |
| `services/catalogo-ms/src/main/java/...` | Codigo del servicio |
| `services/catalogo-ms/src/main/resources/db/migration` | Migraciones Flyway |
| `services/catalogo-ms/README.md` | Operacion y evidencias |

### 3.7.2 Verificacion rapida de base de datos

DEV:

```bash
docker exec -it ecom-postgres-catalogo-dev psql -U ecom -d ecom_catalogo_db
```

Dentro de `psql`:

```sql
\dt
\d categorias
SELECT * FROM categorias;
\q
```

PROD local:

```bash
docker exec -it ecom-postgres-catalogo psql -U ecom -d ecom_catalogo_db -c "\dt"
docker exec -it ecom-postgres-catalogo psql -U ecom -d ecom_catalogo_db -c "SELECT * FROM categorias;"
```

## 4. Crea: actividad autonoma

Fuera del aula, cada estudiante consolida el aprendizaje replicando el patron y preparando evidencias individuales.

Duracion: 4h.

- Replicar el patron en otro servicio del dominio.
- Completar pruebas PowerShell/bash.
- Documentar evidencias individuales.
- Preparar explicacion tecnica del flujo REST y BD.

## 5. Cierre evaluativo

Esta seccion conecta el resultado de aprendizaje de la sesion con el producto que debe evidenciar cada estudiante.

### 5.1 Resultados esperados

Al finalizar la sesion, el estudiante debe demostrar que:

- El microservicio ejecuta en DEV con Maven.
- El microservicio ejecuta en PROD local con Docker.
- PostgreSQL funciona en DEV y PROD local.
- El CRUD de `Categoria` responde por shell.
- Swagger y `/actuator/health` funcionan en DEV.
- Flyway crea la tabla `categorias`.
- El microservicio puede levantar multiples instancias, maximo dos en laboratorio.
- Puede explicar la diferencia entre DEV Maven y PROD Docker.

### 5.2 Evidencias del producto de sesion

Las evidencias deben mostrar el producto declarado en la seccion 1.3:

- Captura o salida de consola de `mvn spring-boot:run`.
- Salida de CRUD probado por PowerShell o bash.
- Salida de Swagger o lista de endpoints disponible.
- Salida de `/actuator/health`.
- Salida de `psql` mostrando tabla `categorias` y registros.
- Salida de `docker compose ps` en PROD local.
- Salida de dos instancias como maximo.
- Breve descripcion del aporte individual.

Comparacion minima que debe defender:

| Aspecto | DEV Maven | PROD Docker |
|---|---|---|
| Aplicacion | Ejecuta en host con `mvn spring-boot:run` | Ejecuta dentro de contenedor |
| Base de datos | PostgreSQL en Docker DEV | PostgreSQL en Docker PROD |
| Puerto del microservicio | Dinamico con `server.port: 0` | Interno `8080` dentro de Docker |
| Acceso externo | Directo al puerto asignado | Por red Docker; luego por Gateway |
| Proposito | Desarrollo, depuracion y cambios rapidos | Ejecucion reproducible y cercana a produccion |

### 5.3 Preguntas de defensa

1. Por que un microservicio debe ser stateless?
2. Que responsabilidad tiene `catalogo-ms`?
3. Como se prueba el servicio sin usar Postman?
4. Que evidencia demuestra que la BD fue usada?
5. Que diferencia hay entre DEV Maven y PROD Docker?
6. Por que en PROD local no se publica directamente el puerto del microservicio?
7. Que parte implementaste o replicaste individualmente?

### 5.4 Checklist de cierre

- [ ] Servicio ejecuta con Maven.
- [ ] PostgreSQL DEV activo.
- [ ] CRUD probado por shell.
- [ ] Health y Swagger verificados.
- [ ] Produccion local con Docker ejecutada.
- [ ] Escalado maximo a dos instancias evidenciado.
- [ ] Evidencia individual registrada.
