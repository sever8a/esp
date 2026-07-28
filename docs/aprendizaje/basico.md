--- 
title: Aprendizaje básico
summary: Herramientas y recursos para aprendizaje básico.
authors:
    - Revisión autorizada
    - Jose Robledano
date: 2026-07-28
---

# Entornos virtuales, `pip` y `conda` — guía breve

## ¿Qué es un entorno virtual de Python?
Un entorno virtual es un directorio aislado que contiene una instalación independiente de Python y sus paquetes. Permite que cada proyecto tenga sus propias dependencias y versiones sin interferir con otros proyectos o con la instalación global del sistema.

### Por qué son importantes
- Evitan conflictos de versiones entre proyectos (por ejemplo, una app necesita `requests==2.25` y otra `requests==2.31`).
- Facilitan la reproducción de entornos (clave para despliegue y colaboración).
- Protegen la instalación global del sistema y reducen la necesidad de privilegios administrativos.

## Ventajas e inconvenientes

Ventajas:
- Aislamiento claro de dependencias por proyecto.
- Reproducibilidad: compartir `requirements.txt` o `environment.yml` permite reconstruir el entorno.
- Menor riesgo de romper otras aplicaciones o la instalación del sistema.

Inconvenientes:
- Ocupan espacio adicional en disco si se crean muchos entornos.
- Gestión extra: hay que crear/activar/desactivar entornos explícitamente.
- En proyectos grandes con paquetes nativos, la instalación puede requerir herramientas del sistema (compiladores) o paquetes binarios.

## Herramientas y comandos básicos

Usando `venv` (incluido en Python estándar):

```bash
python -m venv .venv
# Activar (Linux/macOS)
source .venv/bin/activate
# Activar (Windows PowerShell)
.venv\Scripts\Activate.ps1

pip install -r requirements.txt
pip freeze > requirements.txt
```

Usando `virtualenv` (similar, histórico):

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
```

Exportar/compartir dependencias:
- `pip freeze > requirements.txt`
- `pip install -r requirements.txt`

## `pip` vs `conda` — dos aproximaciones distintas

`pip`:
- Instalador oficial de paquetes Python desde el índice PyPI.
- Funciona bien con paquetes escritos en Python puro o con ruedas binarias (`.whl`) precompiladas.
- Ligero y estándar en la mayoría de proyectos; suele usarse junto a `venv` o herramientas de gestión como `pipenv` o `poetry`.

`conda`:
- Sistema de gestión de paquetes y entornos (Anaconda / Miniconda) que instala paquetes no solo Python, también binarios y dependencias del sistema.
- Ideal para ciencia de datos y paquetes que requieren compilación (NumPy, SciPy, librerías con extensiones C/C++), ya que distribuye binarios preconstruidos por plataforma.
- Permite crear entornos y exportarlos con `environment.yml`.

Comparación por propósitos:
- **Proyectos web y apps Python puras:** `pip` + `venv` es suficiente y más ligero.
- **Ciencia de datos, ML y paquetes con dependencias nativas:** `conda` facilita la instalación y evita problemas de compilación; es común usar `conda` para el entorno base y `pip` dentro del entorno cuando un paquete no está en los canales de conda.

Comandos básicos `conda`:

```bash
conda create -n mi_entorno python=3.10
conda activate mi_entorno
conda install numpy pandas scikit-learn
conda env export > environment.yml
conda env create -f environment.yml
```

## Buenas prácticas
- Mantén un único fichero de dependencias por proyecto (`requirements.txt` o `environment.yml`).
- Usa entornos por proyecto y no la instalación global.
- Para reproducibilidad estricta, fija versiones en el fichero de dependencias.
- Considera `pip-tools` o `poetry` para gestión avanzada de dependencias y bloqueo de versiones.
