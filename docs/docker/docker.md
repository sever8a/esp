--- 
title: Docker
summary: Instalación en diferentes sistemas y sus recursos más útiles.
authors:
    - Revisión autorizada
    - Jose Robledano
date: 2026-07-28
---

# Instalación y gestión de Docker

Este documento describe opciones de instalación de Docker en varios sistemas operativos y cómo gestionar contenedores tanto con Docker Desktop (interfaz gráfica) como con la línea de comandos.

## Requisitos previos
- Hardware compatible con virtualización activada en BIOS/UEFI.
- En Windows, se recomienda usar WSL2 para una integración fluida con herramientas Linux.

## Instalación en Windows

Opción recomendada: Docker Desktop (incluye GUI, Docker Engine y Docker Compose integrado).

- Descargar e instalar desde la web oficial: https://www.docker.com/products/docker-desktop
- Requisitos: Windows 10/11 64-bit, WSL2 recomendado para rendimiento en sistemas Home/Pro.

Para habilitar WSL2 (PowerShell con privilegios de administrador):

```powershell
wsl --install
# Reinicia si es necesario, luego instala una distribución (ej. Ubuntu)
wsl --install -d Ubuntu
```

Después de instalar Docker Desktop, actívalo y en Settings -> Resources -> WSL Integration habilita la integración con las distribuciones que uses.

## Instalación en macOS

Opción recomendada: Docker Desktop para macOS.

- Instalar vía Homebrew (recomendado para usuarios de macOS con Homebrew):

```bash
brew install --cask docker
open /Applications/Docker.app
```

Nota: en Apple Silicon (M1/M2) usa la versión para ARM disponible en la web oficial.

## Instalación en Ubuntu / Debian (paquetes oficiales)

Pasos abreviados para instalar Docker Engine desde el repositorio oficial:

```bash
sudo apt update
sudo apt install ca-certificates curl gnupg lsb-release -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io -y
```

Comprobar la instalación y ejecutar un contenedor de prueba:

```bash
sudo systemctl start docker
sudo systemctl enable docker
sudo docker run --rm hello-world
```

Para evitar `sudo` en cada comando:

```bash
sudo usermod -aG docker $USER
# Cerrar sesión y entrar de nuevo o ejecutar `newgrp docker`
```

## Instalación en CentOS / RHEL / Fedora

Ejemplo simplificado para CentOS/RHEL:

```bash
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install -y docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
sudo systemctl enable docker
sudo docker run --rm hello-world
```

En Fedora, usar `dnf` en lugar de `yum`.

## Instalación en entornos embebidos y microcontroladores

Para dispositivos con recursos limitados existe `MicroPython` o `Tiny Core` y variantes; sin embargo, Docker clásico no suele ejecutarse en microcontroladores. Para Raspberry Pi y ARM compatibles, usar las imágenes oficiales multiarch disponibles en Docker Hub.

## Gestión con Docker Desktop (GUI)

- Fácil administración de imágenes, contenedores, volúmenes y redes desde la interfaz.
- Integración con WSL2 en Windows y acceso a preferencias de recursos (CPU, memoria, disco).
- Panel para logs y terminal integrado por contenedor.

## Gestión mediante línea de comandos (CLI)

Comandos comunes para empezar:

```bash
docker --version
docker pull nginx:latest
docker run --name web -d -p 8080:80 nginx:latest
docker ps
docker logs -f web
docker exec -it web /bin/bash
docker stop web && docker rm web
docker images
docker rmi <imagen>
docker build -t miapp:latest .
```

Usando Docker Compose (plugin integrado en Docker 3.x+ o `docker-compose` clásico):

```bash
docker compose up -d
docker compose down
```

Consejos prácticos
- Usa `docker system prune -a` con precaución para liberar espacio.
- Mantén las imágenes actualizadas y limpia contenedores e imágenes no usados periódicamente.
- Usa volúmenes para persistencia de datos: `docker run -v mi_vol:/data ...`.

## Recursos y referencias
- Documentación oficial Docker: https://docs.docker.com/
- Docker Desktop: https://www.docker.com/products/docker-desktop
- Docker Hub: https://hub.docker.com/
