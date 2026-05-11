# Instalación con Docker y PostgreSQL

n8n recomienda Docker para la mayoría de escenarios de auto-hosting por su aislamiento y facilidad de despliegue. Este proyecto usa PostgreSQL como única base de datos soportada.

## Prerrequisitos
- Docker Engine y Docker Compose instalados
- Puerto 5678 disponible en el host
- Conocer tu zona horaria (por ejemplo: "America/Bogota")

## Inicio rápido

Crea un volumen persistente y levanta el contenedor:

```
docker volume create n8n_data

docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -e GENERIC_TIMEZONE="<TU_ZONA_HORARIA>" \
  -e TZ="<TU_ZONA_HORARIA>" \
  -e N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true \
  -e N8N_RUNNERS_ENABLED=true \
  -e DB_TYPE=postgresdb \
  -e DB_POSTGRESDB_DATABASE=<DB_NAME> \
  -e DB_POSTGRESDB_HOST=<DB_HOST> \
  -e DB_POSTGRESDB_PORT=<DB_PORT> \
  -e DB_POSTGRESDB_USER=<DB_USER> \
  -e DB_POSTGRESDB_SCHEMA=<DB_SCHEMA> \
  -e DB_POSTGRESDB_PASSWORD=<DB_PASSWORD> \
  -v n8n_data:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```

- Mapea 5678/tcp al host
- Configura la zona horaria para el sistema y los nodos de agenda
- Enforce de permisos seguros del archivo de configuración
- Habilita Task Runners (recomendado)
- Persiste el directorio `/home/node/.n8n` (claves, logs, assets, etc.)

Accede a n8n en: http://localhost:5678

## Docker Compose (PostgreSQL)

Consulta `docker/docker-compose.postgres.yml` y `.env` para variables.

```bash
docker compose -f docker/docker-compose.n8n.yml -f docker/docker-compose.postgres.yml --env-file docker/.env up -d
```

## Notas
- Usa PostgreSQL como base de datos principal en este proyecto
- Asegura el acceso (SSL/Reverse Proxy/Firewall)
- Realiza backups periódicos de la base de datos y del directorio `.n8n`
