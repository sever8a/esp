--- 
title: Aprendizaje medio
summary: Herramientas y recursos para aprendizaje medio.
authors:
    - Revisión autorizada
    - Jose Robledano
date: 2026-07-28
---

# Uso de `pip` y comportamiento de `!` / `%` en notebooks

## Instrucciones básicas de `pip`
`pip` es el instalador estándar de paquetes de Python desde PyPI. Comandos esenciales:

- Instalar un paquete:

```bash
pip install nombre_paquete
```

- Instalar una versión concreta:

```bash
pip install nombre_paquete==1.2.3
```

- Actualizar un paquete:

```bash
pip install --upgrade nombre_paquete
```

- Desinstalar un paquete:

```bash
pip uninstall nombre_paquete
```

- Listar paquetes instalados:

```bash
pip list
```

- Información sobre un paquete:

```bash
pip show nombre_paquete
```

- Comprobar dependencias conflictivas:

```bash
pip check
```

Importante para entornos con kernels (notebooks): es preferible usar la magia `%pip` o `python -m pip` para asegurar que la instalación se aplica al intérprete de Python que está ejecutando el kernel:

```python
import sys
!{sys.executable} -m pip install paquete
# o
%pip install paquete
```

## Crear y usar `requirements.txt`
Para capturar las dependencias actuales del entorno y compartirlas:

```bash
pip freeze > requirements.txt
```

Para instalar desde ese fichero en otro entorno:

```bash
pip install -r requirements.txt
```

Consejos:
- Fijar versiones en `requirements.txt` (ej. `package==1.2.3`) para reproducibilidad.
- Para proyectos más complejos considere `pip-tools`, `poetry` o `pipenv` para manejo de versiones y bloqueo.

## `!` vs `%` en JupyterHub / JupyterLab (y en notebooks en general)

- `!` (prefijo de celda o línea) ejecuta un comando de shell desde la celda. Por ejemplo:

```python
!ls -la
!pip install paquete
```

Ventaja: permite usar utilidades del sistema directamente. Inconveniente: cuando usas `!pip install` puede instalar en el entorno del sistema o en un intérprete distinto al kernel; por eso el uso de `%pip` o `python -m pip` es más fiable dentro de notebooks.

- `%` (magics de línea) y `%%` (magics de celda) son comandos especiales de IPython que realizan tareas dentro del kernel y tienen funcionalidades específicas. Ejemplos:

```python
%timeit sum(range(1000))  # línea-magic para medir tiempo
%%bash
echo "Esto se ejecuta como un script bash completo"
```

Magias útiles relacionadas con instalación y entorno:
- `%pip install paquete` — ejecuta la instalación asegurando que el paquete queda disponible en el kernel actual.
- `%conda install paquete` — si el kernel se ejecuta dentro de un entorno `conda`, esta magia invoca `conda` desde el kernel.

Resumen práctico:
- Usa `!` para comandos rápidos de shell cuando no afecte al entorno del kernel.
- Prefiere `%pip` o `python -m pip` para instalar paquetes desde un notebook y garantizar que se instalan en el intérprete correcto.
- Usa `%%bash` o `%%bash -x` cuando necesites ejecutar scripts de shell completos en una celda.
