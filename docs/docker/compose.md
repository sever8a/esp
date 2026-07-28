--- 
title: Compose
summary: Manera rápida de desplegar servicios y combinarlos.
authors:
    - Revisión autorizada
    - Jose Robledano
date: 2026-07-28
---

# Docker Compose: qué es y cómo usarlo (guía rápida)

Docker Compose es una herramienta para definir y ejecutar aplicaciones multicontenedor mediante un archivo YAML (`docker-compose.yml`). Permite describir los servicios, redes y volúmenes necesarios para una aplicación y administrarlos con comandos sencillos.

## Concepto por niveles

### Nivel 1 — Idea rápida
- Un único archivo (`docker-compose.yml`) describe varios contenedores y cómo se comunican.
- Un comando (`docker compose up`) levanta toda la aplicación.

### Nivel 2 — Componentes principales
- **Servicios:** cada servicio representa un contenedor (imagen, puertos, variables de entorno).
- **Redes:** cómo se comunican los servicios entre sí.
- **Volúmenes:** para persistencia de datos entre reinicios.

### Nivel 3 — Ventajas
- Orquestación local simple para desarrollo y pruebas.
- Reproducibilidad: el equipo usa la misma configuración.
- Integración limpia con pipelines CI/CD.

## Formato básico y ejemplo mínimo
Archivo de ejemplo `docker-compose.yml` para una app web con Nginx y una base de datos Postgres:

```yaml
version: '3.8'
services:
    db:
        image: postgres:15
        environment:
            POSTGRES_USER: ejemplo
            POSTGRES_PASSWORD: ejemplo123
            POSTGRES_DB: ejemplo_db
        volumes:
            - db_data:/var/lib/postgresql/data

    web:
        image: nginx:latest
        ports:
            - "8080:80"
        depends_on:
            - db

volumes:
    db_data:
```

Guarda este contenido en `docker-compose.yml` y ejecuta:

```bash
docker compose up -d
```

## Comandos básicos (CLI)

- Levantar servicios en segundo plano:

```bash
docker compose up -d
```

- Ver estados de servicios:

```bash
docker compose ps
```

- Ver logs en tiempo real:

```bash
docker compose logs -f
docker compose logs -f web
```

- Abrir una shell en un servicio:

```bash
docker compose exec web /bin/bash
```

- Parar y eliminar recursos:

```bash
docker compose down
```

- Reconstruir imágenes (cuando el `Dockerfile` cambia):

```bash
docker compose up -d --build
```

- Forzar recreación y limpiar volúmenes (con precaución):

```bash
docker compose down -v
```

## Opciones avanzadas y buenas prácticas
- Usa variables de entorno en un archivo `.env` para no incluir secretos en `docker-compose.yml`.
- Versionado: `version: '3.8'` o superior según características necesarias.
- Multi-stage builds: construir imágenes pequeñas usando `build:` y `Dockerfile` con múltiples etapas.
- Escalado local (útil en pruebas):

```bash
docker compose up -d --scale web=3
```

Nota: para producciones a gran escala usar Kubernetes, Docker Swarm o un orquestador adecuado.

## Integración con CI/CD
- Usa `docker compose pull` y `docker compose up -d --build` en pasos automatizados.
- Validar configuración con `docker compose config` antes de desplegar.

## Recursos útiles
- Documentación oficial: https://docs.docker.com/compose/
- Referencia de sintaxis: https://docs.docker.com/compose/compose-file/
