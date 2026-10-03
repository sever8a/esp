--- 
title: Jupyter Notebooks
summary: Formato de código que permite la ejecución modluar, comprobando los resultados.
authors:
    - Revisión autorizada
    - Jose Robledano
date: 2026-07-28
---

# Jupyter Notebooks: guía para principiantes

Jupyter Notebook es un entorno interactivo basado en web que permite combinar código ejecutable, visualizaciones y documentación (markdown) en un mismo documento llamado cuaderno (notebook). Es ampliamente usado en data science, enseñanza y prototipado.

## Funcionamiento básico
- **Celdas:** un notebook se compone de celdas de código y celdas de markdown. Las celdas de código se envían al `kernel` (intérprete) para ejecutarse; las celdas de markdown contienen texto formateado, títulos y ecuaciones.
- **Kernel:** proceso que ejecuta el código (por ejemplo, un kernel Python). El kernel mantiene el estado (variables, módulos cargados) entre celdas.
- **Ejecución por celdas:** puedes ejecutar celdas de forma independiente y ver resultados inmediatamente; el orden de ejecución importa (no siempre coincide con el orden visual).
- **Salida rica:** gráficos, tablas, imágenes, audio y widgets pueden mostrarse inline como salidas de las celdas.

## Características fundamentales
- **Interactividad:** ejecución paso a paso, re-ejecución rápida y exploración iterativa de datos.
- **Visualización integrada:** bibliotecas como Matplotlib, Seaborn, Plotly y Bokeh muestran figuras embebidas.
- **Magics y comandos especiales:** comandos como `%timeit`, `%matplotlib inline` o `%%bash` facilitan tareas comunes.
- **Exportación:** convertir notebooks a HTML, PDF, slides o scripts con `nbconvert`.
- **Extensiones y JupyterLab:** JupyterLab es la interfaz moderna que añade paneles; extensiones amplían funcionalidades (ej. variable inspector, git integration).

## Posibilidades didácticas
- **Material interactivo para clases:** combinar teoría (markdown) con ejercicios ejecutables y ejemplos resueltos.
- **Laboratorios guiados:** proporcionar notebooks con celdas incompletas para que el estudiantado las rellene y pruebe.
- **Evaluación automática:** integrar con herramientas de auto-evaluación (nbgrader) para crear y corregir ejercicios.
- **Compartir fácilmente:** subir a GitHub, usar Binder para ejecutar notebooks sin instalar nada, o Google Colab para proporcionar acceso a GPU/TPU.

## Uso en proyectos de mayor envergadura
- **Prototipado y experimentación:** notebooks son ideales para explorar datos y prototipos rápidos antes de convertir código a módulos reproducibles.
- **Pipelines y reproducibilidad:** integrar notebooks en pipelines mediante `papermill` (parametrización y ejecución automatizada) o convertir a scripts para producción.
- **Control de versiones:** los notebooks son JSON; usa `nbdime` para diffs, `jupytext` para sincronizar con scripts `.py` y mantener historial legible en Git.
- **Despliegue:** exportar resultados o encapsular modelos entrenados en scripts/paquetes para despliegue en servidores o contenedores (Docker).

## Uso de Google Colab y almacenamiento de cuadernos

Google Colab permite crear y ejecutar notebooks desde el navegador, sin instalar Jupyter en el equipo. El código se ejecuta en un entorno alojado por Google y puede usar Python y bibliotecas habituales. Para empezar, accede a [Google Colab](https://colab.research.google.com/) con una cuenta de Google.

### Crear y ejecutar un notebook

Selecciona **Archivo > Nuevo cuaderno** para abrir uno vacío. Cada celda puede contener código o texto en Markdown. Escribe, por ejemplo, este código en una celda y ejecútala con el botón de reproducción o `Mayús+Intro`:

```python
mensaje = "Hola desde Colab"
print(mensaje)
```

La salida aparecerá debajo de la celda. Puedes añadir una celda de texto para explicar el ejemplo y guardar el cuaderno con un nombre reconocible.

### Guardar y abrir cuadernos con Google Drive

Al crear un cuaderno desde Colab, normalmente se guarda en la carpeta **Colab Notebooks** de Google Drive. También puedes abrir un cuaderno existente desde **Archivo > Abrir cuaderno > Google Drive**. Para conservar los cambios, usa **Archivo > Guardar** o `Ctrl+S` (`Cmd+S` en macOS); comprueba que el cuaderno aparece en Drive.

Para acceder a otros archivos guardados en Drive desde el código, monta la unidad:

```python
from google.colab import drive
drive.mount('/content/drive')
```

Sigue el proceso de autorización que muestra Colab. Después, los archivos de Drive estarán disponibles bajo `/content/drive/MyDrive/`. Por ejemplo, para listar una carpeta:

```python
import os

carpeta = '/content/drive/MyDrive'
print(os.listdir(carpeta)[:10])
```

### Usar un cuaderno o documentos locales

Para abrir un notebook `.ipynb` que está en el equipo, selecciona **Archivo > Abrir cuaderno > Subir** y elige el archivo. También puedes crear o descargar una copia desde **Archivo > Descargar > Descargar .ipynb**. Los cambios en una copia subida no actualizan automáticamente el archivo original del equipo; vuelve a descargarla para guardarlos localmente.

Para aportar un documento local a una sesión, puedes seleccionarlo desde el panel **Archivos** de Colab mediante el botón de subir, o usar:

```python
from google.colab import files

archivos = files.upload()  # Abre un selector de archivos locales
```

Por ejemplo, si subes `datos.csv`, puedes leerlo con pandas:

```python
import pandas as pd

datos = pd.read_csv('datos.csv')
print(datos.head())
```

Los archivos subidos de esta forma quedan en el entorno temporal de ejecución, no en Drive. Pueden desaparecer al reiniciar o desconectar la sesión; guarda los resultados importantes en Drive o descárgalos. Para leer un documento guardado en Drive, usa su ruta bajo `/content/drive/MyDrive/` en lugar de subirlo de nuevo.

## Comandos básicos

Instalar Jupyter:

```bash
pip install jupyterlab
# o para el clásico notebook
pip install notebook
```

Iniciar servidor local (JupyterLab recomendado):

```bash
jupyter lab
# o
jupyter notebook
```

Exportar a HTML:

```bash
jupyter nbconvert --to html mi_cuaderno.ipynb
```

Ejecutar un notebook con parámetros (papermill):

```bash
pip install papermill
papermill input.ipynb output.ipynb -p parametro1 valor
```

## Buenas prácticas
- Documenta claramente: usa títulos, explicaciones y comentarios en markdown para que el notebook sea entendible.
- Mantén notebooks limpios: evita celdas con salidas gigantes o datos sensibles y divide el trabajo en funciones reutilizables cuando el código crece.
- Versiona con `jupytext` (sincroniza `.ipynb` con `.py`) para facilitar revisión por pares.
- Para producción, extrae lógica en módulos y usa notebooks solo como interfaz de experimentación o reportes.


