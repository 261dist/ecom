# orden-py

Laboratorio temporal en Python para probar Kafka con un producer y un consumer simples.

La carpeta se llama `orden-py-del` porque es un proyecto temporal.

## Componentes

- `app/producer_ordenes.py`: publica eventos en `orden-eventos`
- `app/consumer_ordenes.py`: consume eventos de `orden-eventos`
- `docker-compose-dev.yml`: contenedor Python conectado a Kafka dev
- `Dockerfile`: imagen base del laboratorio

## Requisitos

Kafka dev debe estar levantado:

```powershell
cd C:\ms1\ProyectosMS2026\kafka
docker compose -f docker-compose-dev.yml up -d
```

El contenedor Python usa:

- red Docker: `kafka-ms-dev-net`
- broker interno: `kafka:9092`

## Levantar el laboratorio

```powershell
cd C:\ms1\ProyectosMS2026\orden-py-del
docker compose -f docker-compose-dev.yml up -d
```

Validar:

```powershell
docker compose -f docker-compose-dev.yml ps
```

## Hot reload

El compose monta:

```text
./app -> /app
```

Puedes editar los scripts localmente y volver a ejecutarlos dentro del contenedor sin reconstruir la imagen.

## Ejecutar producer

```powershell
docker compose -f docker-compose-dev.yml exec orden-py python /app/producer_ordenes.py
```

Publica un evento cada 2 segundos con este formato:

```json
{
  "tipoEvento": "orden.creada",
  "ordenId": 123,
  "total": 250.0,
  "estado": "PENDIENTE",
  "origen": "python",
  "timestamp": 1713350000000
}
```

## Ejecutar consumer

En otra terminal:

```powershell
docker compose -f docker-compose-dev.yml exec orden-py python /app/consumer_ordenes.py
```

El consumer usa:

```text
orden-py-group
```

Los logs salen con:

```text
service=orden-py
```

## Detener

```powershell
docker compose -f docker-compose-dev.yml down
```

## Estado de avance

- [x] Laboratorio Python temporal para Kafka
- [x] Producer Python hacia `orden-eventos`
- [x] Consumer Python desde `orden-eventos`
- [x] Conexion por red Docker `kafka-ms-dev-net`
- [x] Broker interno `kafka:9092`
- [x] Hot reload mediante volumen `./app:/app`
- [ ] Empaquetado como servicio definitivo
- [ ] Integracion formal con pipeline de datos

---

## Tag sugerido

```bash
git tag -a vs09-kafka -m "eda con vs09-kafka"
git push origin vs09-kafka
```
