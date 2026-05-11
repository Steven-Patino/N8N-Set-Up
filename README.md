# N8N SET UP– Tutorial Teórico (ES)

**Este repositorio es una guía de aprendizaje para ejecutar y entender n8n con Docker.**
Incluye conceptos, arquitectura, instalación, configuración, seguridad y ejemplos prácticos.

## ✅ Qué encontrarás aquí

- Introducción a n8n y su propósito.
- Arquitectura y componentes clave.
- Instalación con Docker usando PostgreSQL.
- Actualización y mantenimiento de contenedores.
- Conexión de webhooks en desarrollo usando túneles.
- Configuración segura con variables de entorno.
- Buenas prácticas de seguridad y escalado.
- Logs, monitoreo y resolución de problemas.
- Ejercicios teóricos para reforzar el aprendizaje.
- Recursos oficiales y comunidad.

## 📁 Estructura del repositorio

```
.
├─ README.md
├─ docs/
│  ├─ 01-que-es-n8n.md
│  ├─ 02-arquitectura.md
│  ├─ 03-instalacion-docker.md
│  ├─ 04-postgresql.md
│  ├─ 05-actualizacion.md
│  ├─ 06-tunel-webhooks.md
│  ├─ 07-configuracion.md
│  ├─ 08-seguridad.md
│  ├─ 09-escalado-rendimiento.md
│  └─ 10-logs-monitoreo.md
├─ docker/
│  ├─ docker-compose.n8n.yml
│  ├─ docker-compose.postgres.yml
│  └─ .env
├─ scripts/
│  └─ commands.md
└─ .env-template/
   ├─ .env.example
   └─ README.md
```

## 🛠 Requisitos previos

- Docker y Docker Compose instalados.
- Conocimientos básicos de contenedores y redes.
- Manejo de variables de entorno y seguridad de credenciales.
- Para producción: bases sólidas de SSL, firewall y administración de recursos.

> Si quieres una solución administrada, considera n8n Cloud.

## 🚀 Empezar rápido

### 1) Clona el proyecto

```bash
git clone <URL_DE_TU_REPO> n8n-starter
cd n8n-starter
```

### 2) Crea tu archivo de entorno

Copia la plantilla en el directorio `docker/`:

```bash
cp .env-template/.env.example docker/.env
```

Edita `docker/.env` y ajusta al menos:
- `TZ` y `GENERIC_TIMEZONE`
- `WEBHOOK_URL`
- `DB_POSTGRESDB_HOST`, `DB_POSTGRESDB_PORT`, `DB_POSTGRESDB_DATABASE`, `DB_POSTGRESDB_USER`, `DB_POSTGRESDB_PASSWORD`
- `N8N_ENCRYPTION_KEY` en entornos persistentes

### 3) Elige tu despliegue

#### PostgreSQL (único modo soportado por este proyecto)

```bash
docker compose -f docker/docker-compose.n8n.yml -f docker/docker-compose.postgres.yml --env-file docker/.env up -d
```

### 4) Verifica el estado

```bash
docker compose -f docker/docker-compose.n8n.yml -f docker/docker-compose.postgres.yml --env-file docker/.env ps
```

### 5) Revisa los logs

```bash
docker compose -f docker/docker-compose.n8n.yml -f docker/docker-compose.postgres.yml --env-file docker/.env logs -f n8n
```

### 6) Accede a n8n

Abre en tu navegador:

```text
http://localhost:5678
```

### 7) Detén los servicios

```bash
docker compose -f docker/docker-compose.n8n.yml -f docker/docker-compose.postgres.yml --env-file docker/.env down
```

## ⚠️ Recomendaciones de seguridad

- Nunca subas `docker/.env` con credenciales reales.
- Mantén `N8N_ENCRYPTION_KEY` configurada para migraciones y seguridad.
- Usa un proxy inverso con HTTPS si expones n8n en internet.
- Ajusta `WEBHOOK_URL` a tu dominio público seguro.

## 📘 Documentación interna

- `docs/03-instalacion-docker.md` — Instalación con Docker y PostgreSQL.
- `docs/04-postgresql.md` — Uso de PostgreSQL con n8n.
- `docs/06-tunel-webhooks.md` — Túnel para webhooks en desarrollo.
- `docs/08-seguridad.md` — Buenas prácticas de seguridad.
- `scripts/commands.md` — Comandos útiles rápidos.

## 📌 Nota importante

La carpeta `.env-template` contiene la plantilla de variables de entorno. Copia ese ejemplo antes de comenzar y personaliza las variables según tu entorno.

## 📄 Licencia

Contenido con fines educativos. Verifica licencias y requisitos de n8n antes de usarlo en producción.
