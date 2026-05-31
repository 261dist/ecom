# S9 - Arquitectura orientada a eventos con Kafka

## Ubicacion en el curso

- Unidad: U2 - Sistema distribuido robusto e integrado.
- Producto de unidad: Sistema distribuido seguro, resiliente, observable, orientado a eventos e integrado con frontend.
- Avance del producto en esta sesion: comunicacion asincrona mediante eventos.

## Proposito

Incorporar Kafka para desacoplar procesos entre `orden-ms` y `pago-ms`.

## Resultado de aprendizaje

El estudiante crea topics, publica eventos y verifica consumo asincrono.

## Producto de sesion

Kafka operativo con topics `orden-eventos` y `pago-eventos`, producer y consumer funcionales.

## Concepto distribuido clave

La mensajeria asincrona desacopla emisor y receptor. El productor no necesita esperar a que el consumidor procese inmediatamente.

## Implementacion en el proyecto

`orden-ms` publica eventos de orden y `pago-ms` consume esos eventos para generar pagos.

## Pasos para construir el producto de sesion

1. Levantar Kafka y Kafka UI.
2. Crear los topics necesarios para el flujo de negocio.
3. Definir el evento que publicara el productor.
4. Implementar el producer en el microservicio origen.
5. Publicar el evento despues de confirmar la operacion de negocio.
6. Implementar el consumer en el microservicio destino.
7. Persistir el resultado generado por el evento.
8. Verificar topics, logs del producer, logs del consumer y registros en BD.

## Archivos involucrados

| Archivo | Proposito |
|---|---|
| `kafka/compose-dev.yml` | Kafka DEV |
| `services/orden-ms/src/main/java/.../ProductorOrden.java` | Producer |
| `services/pago-ms/src/main/java/.../ConsumidorPago.java` | Consumer |

## Comandos de ejecucion

### PowerShell

```powershell
cd kafka
docker compose -f compose-dev.yml up -d
docker compose -f compose-dev.yml exec kafka bash
```

Dentro del broker:

```bash
/opt/kafka/bin/kafka-topics.sh --create --topic orden-eventos --bootstrap-server kafka:9092 --partitions 1 --replication-factor 1
/opt/kafka/bin/kafka-topics.sh --create --topic pago-eventos --bootstrap-server kafka:9092 --partitions 1 --replication-factor 1
/opt/kafka/bin/kafka-topics.sh --list --bootstrap-server kafka:9092
```

### bash macOS/Linux

```bash
cd kafka
docker compose -f compose-dev.yml up -d
docker compose -f compose-dev.yml exec kafka bash
```

## Verificacion funcional

Crear una orden por Gateway y verificar que `pago-ms` registra un pago.

## Observabilidad y diagnostico

- Kafka UI: `http://localhost:41085`.
- Listar topics.
- Revisar logs de `orden-ms` y `pago-ms`.
- Revisar consumer groups si aplica.

## Verificacion de base de datos

```powershell
docker exec -it ecom-postgres-orden-dev psql -U ecom -d ecom_orden_db -c "SELECT * FROM ordenes;"
docker exec -it ecom-postgres-pago-dev psql -U ecom -d ecom_pago_db -c "SELECT * FROM pagos;"
```

## Evidencia esperada

- Topics creados.
- Evento publicado.
- Pago generado por consumo de evento.

## Errores frecuentes

| Problema | Causa probable | Solucion |
|---|---|---|
| No aparece pago | Consumer apagado | Levantar `pago-ms` |
| Topic no existe | No fue creado o autocreacion fallo | Crear topic manual |

## Preguntas de defensa

1. Que diferencia hay entre Feign y Kafka?
2. Por que Kafka desacopla servicios?
3. Que evidencia muestra que el evento fue consumido?

## Checklist de cierre

- [ ] Kafka activo.
- [ ] Topics creados.
- [ ] Orden creada.
- [ ] Pago generado.
