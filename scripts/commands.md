# Comandos útiles

Este archivo ofrece ejemplos rápidos para ejecutar n8n con Docker y Docker Compose.

## Docker Run (rápido)

Usa este comando cuando quieras validar rápidamente el contenedor de n8n sin Docker Compose.

```bash
docker volume create n8n_data

docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -e GENERIC_TIMEZONE="America/Bogota" \
  -e TZ="America/Bogota" \
  -e N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true \
  -e N8N_RUNNERS_ENABLED=true \
  -v n8n_data:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```

## Docker Compose (Postgres)

Ejecuta n8n junto a PostgreSQL usando ambos archivos Compose.

```bash
docker compose -f docker/docker-compose.n8n.yml -f docker/docker-compose.postgres.yml --env-file docker/.env up -d
```

## Actualización

Para actualizar la imagen de n8n, descárgala de Docker Hub y vuelve a iniciar tu contenedor.

```bash
docker pull docker.n8n.io/n8nio/n8n
# luego reinicia el contenedor con tus parámetros
```
