--- 
title: VSCode
summary: VScode una herramienta versátil para el desarrollo, en múltiples ecosistemas.
authors:
    - Revisión autorizada
    - Jose Robledano
date: 2026-07-28
---

# Desarrollo Python en VS Code con Dev Containers y Docker

Esta guía explica cómo configurar un entorno de desarrollo local para Python usando Visual Studio Code, Dev Containers (Remote - Containers) y Docker. Incluye requisitos, pasos de instalación y comprobaciones básicas.

## Requisitos
- **Docker:** Docker Desktop (Windows/macOS) o Docker Engine (Linux) instalado y funcionando. En Windows, habilitar WSL2 para mejor integración.
- **Visual Studio Code:** última versión estable de VS Code.
- **Extensiones VS Code:** instalar `Remote - Containers` (parte de `Dev Containers`), `Python` (Microsoft) y opcionalmente `Pylance`, `Docker`.

## Pasos de instalación

1. Instalar Docker

Windows / macOS:
```powershell
# Descargar Docker Desktop desde https://www.docker.com/products/docker-desktop
# Ejecutar el instalador y seguir instrucciones
```

Linux (ej. Ubuntu):
```bash
sudo apt update
sudo apt install ca-certificates curl gnupg lsb-release -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io -y
sudo usermod -aG docker $USER
# Cerrar sesión e iniciar de nuevo
```

2. Instalar Visual Studio Code
- Descargar e instalar desde https://code.visualstudio.com/

3. Instalar extensiones en VS Code
- Abre VS Code > Extensiones y busca e instala:
    - `Dev Containers` (o `Remote - Containers`)
    - `Python` (Microsoft)
    - `Pylance` (recomendado)
    - `Docker` (opcional)

## Crear un Dev Container para un proyecto Python

1. En tu proyecto abre la paleta de comandos (`Ctrl+Shift+P`) y selecciona `Dev Containers: Add Dev Container Configuration Files`.
2. Elige una plantilla (por ejemplo, `Python` -> `Python 3`).
3. Esto crea una carpeta `.devcontainer/` con al menos `devcontainer.json` y un `Dockerfile` o `docker-compose.yml` según la configuración.

Ejemplo mínimo de `.devcontainer/devcontainer.json`:

```json
{
    "name": "Python 3",
    "build": {
        "dockerfile": "Dockerfile"
    },
    "settings": {
        "python.pythonPath": "/usr/local/bin/python"
    },
    "extensions": [
        "ms-python.python",
        "ms-python.vscode-pylance"
    ],
    "forwardPorts": [8000]
}
```

Ejemplo mínimo de `.devcontainer/Dockerfile`:

```Dockerfile
FROM python:3.10-slim
RUN pip install --upgrade pip
WORKDIR /workspace
```

4. Abrir en el contenedor
- En VS Code: `Dev Containers: Reopen in Container`. VS Code construirá la imagen y abrirá el proyecto dentro del contenedor.

## Comprobaciones básicas de funcionamiento
- Verificar que VS Code detecta el intérprete Python dentro del contenedor (barra inferior -> selección de intérprete).
- Abrir un terminal integrado (`Ctrl+ñ` o `Terminal > New Terminal`) y ejecutar:

```bash
python --version
pip list
```

- Crear y ejecutar un script de prueba `hello.py`:

```python
print("Hola desde el Dev Container")
```

Ejecutar en terminal:

```bash
python hello.py
```

## Buenas prácticas y consejos
- Añade `requirements.txt` o `pyproject.toml` y actualiza la imagen (`Dockerfile`) para instalar dependencias en el build.
- Usa `docker-compose` cuando necesites servicios adicionales (Postgres, Redis) y referencia `docker-compose.yml` en `devcontainer.json`.
- Mantén `.devcontainer/` en el repositorio para reproducibilidad del entorno de desarrollo.

¿Quieres que genere un `Dockerfile` y `devcontainer.json` más completos para un proyecto Django o FastAPI como ejemplo? 
