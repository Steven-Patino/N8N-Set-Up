# `.env-template`

Esta carpeta contiene una plantilla de variables de entorno para usar con los archivos Docker Compose del proyecto.

## Uso

1. Copia el archivo de plantilla a `docker/.env`:

```bash
cp .env-template/.env.example docker/.env
```

2. Ajusta valores como `TZ`, `GENERIC_TIMEZONE`, `WEBHOOK_URL`, `DB_POSTGRESDB_PASSWORD` y otros antes de iniciar los servicios.

## Nota de seguridad

- No guardes secretos reales en el repositorio.
- Mantén `docker/.env` fuera del control de versiones si contiene credenciales sensibles.
