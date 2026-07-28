--- 
title: Aprendizaje avanzado
summary: Herramientas y recursos para aprendizaje avanzado.
authors:
    - Revisión autorizada
    - Jose Robledano
date: 2026-07-28
---

# Entornos virtuales y gestión avanzada de dependencias para equipos

Esta sección cubre prácticas avanzadas para usar entornos virtuales, gestionar librerías y coordinar versiones y código en equipos de desarrollo.

## Entornos por proyecto y reproducibilidad
- Mantén un entorno por proyecto (no por máquina) para evitar "works on my machine".
- Prefiere herramientas que generen ficheros de bloqueo (`poetry.lock`, `Pipfile.lock`, `poetry`/`pip-tools`/`pipenv`) o `requirements.txt` generados por `pip-compile` para fijar versiones transitivas.
- Para máxima reproducibilidad en CI/producción, construye ruedas (`.whl`) o imágenes de contenedor con las dependencias preinstaladas.

Ejemplo de flujo reproducible con `pip-tools`:

```bash
pip install pip-tools
pip-compile requirements.in   # genera requirements.txt con dependencias resueltas
pip-sync requirements.txt     # instala exactamente esas versiones
```

## Estrategias de versionado y releases
- Usa semantic versioning (SemVer) para releases (`MAJOR.MINOR.PATCH`).
- Automatiza el versionado con herramientas como `setuptools_scm` o `versioneer` que extraen la versión de las etiquetas Git.
- Crea releases a partir de ramas protegidas y etiqueta (`git tag -a v1.2.3 -m "release v1.2.3"`) para que CI genere artefactos (wheels, sdists).

## Integración continua (CI) y pruebas
- Ejecuta en CI la creación del entorno (usar caches de paquetes), instalación de dependencias, linters, pruebas unitarias e integración, y generación de artefactos.
- Caché de dependencias: en GitHub Actions, cachea pip or conda packages y pip wheels para acelerar builds.
- Usa matrices en CI para probar varias versiones de Python/depedencias.

Ejemplo básico de pasos CI (pseudoyaml):

```yaml
- name: Test
    uses: actions/checkout@v4
- name: Set up Python
    uses: actions/setup-python@v4
    with: {python-version: '3.10'}
- name: Install deps
    run: |
        pip install pip-tools
        pip-compile requirements.in
        pip install -r requirements.txt
- name: Run tests
    run: pytest -q
```

## Control de dependencias y seguridad
- Automatiza actualizaciones con herramientas como Dependabot o Renovate; valida cambios en PRs con pruebas automáticas.
- Escanea vulnerabilidades con `safety`, `pip-audit` o integraciones SCA en CI.
- Usa `constraints.txt` para forzar versiones seguras en entornos corporativos.

## Entornos híbridos y binarios nativos
- Para paquetes con dependencias nativas (librerías en C/Fortran), considera `conda` o ruedas precompiladas (`manylinux`/`macos` wheels) para evitar compilaciones en desarrolladores. Mantén instrucciones de build si es necesario.

## Contenedores como entorno de desarrollo estándar
- Define una imagen base (Dockerfile) con las dependencias del proyecto y usa Dev Containers o reproducibilidad en CI. Esto minimiza diferencias entre entornos locales y producción.
- Publica imágenes de desarrollo en un registry privado con tags por versión (ej. `registry.example.com/project:dev`, `:v1.2.3`).

## Flujo de trabajo en equipo y políticas de código
- Rama principal protegida: exige PRs revisados y pruebas verdes antes de merge.
- Pull Requests pequeños y atómicos facilitan revisiones y reducen conflictos.
- Usa `pre-commit` para formateo (`black`), comprobaciones de estilo (`flake8`), y hooks de seguridad antes de crear PRs.
- Definir convenciones de commits (Conventional Commits) facilita generación de changelogs y releases automáticos.

Ejemplo `.pre-commit-config.yaml` mínimo:

```yaml
repos:
- repo: https://github.com/psf/black
    rev: 24.1.0
    hooks:
    - id: black
- repo: https://github.com/pre-commit/mirrors-flake8
    rev: v6.0.0
    hooks:
    - id: flake8
```

## Pruebas, moleculas de integración y entornos efímeros
- Usa `tox` o `nox` para automatizar matrices de pruebas locales y en CI.
- Para integración con bases de datos o servicios externos, levanta servicios efímeros mediante `docker-compose` en CI o mockea dependencias.

## Gestión de versiones de código y despliegue
- Automatiza builds y despliegues por tag de release en CI; publica paquetes (PyPI, Artifactory) y contenedores.
- Mantén changelogs y notas de release; usa GitHub Releases para adjuntar artefactos.

## Documentación y onboarding
- Incluye instrucciones de setup reproducible en `CONTRIBUTING.md` y scripts `make setup` o `scripts/bootstrap.sh` que creen el entorno y preinstalen herramientas de desarrollo.
- Provee un `devcontainer` o un `docker-compose.dev.yml` para onboarding rápido.

## Resumen de recomendaciones
- Fija versiones y usa lockfiles para reproducibilidad.
- Automatiza versiones, pruebas y despliegues en CI.
- Usa contenedores para minimizar diferencias entre desarrolladores y producción.
- Aplica pre-commit, code review y políticas de ramas para mantener calidad del código.
