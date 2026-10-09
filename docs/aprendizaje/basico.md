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
- **Ventajas:** acceso al amplio catálogo de PyPI, instalación sencilla y compatibilidad con el flujo estándar de Python. Es una buena opción cuando el proyecto depende principalmente de paquetes Python y estos ofrecen ruedas para la plataforma.
- **Inconvenientes:** no administra por sí solo el intérprete ni todas las dependencias externas al ecosistema Python. Si no hay una rueda compatible, puede ser necesario compilar el paquete y disponer de herramientas del sistema.

`conda`:
- Sistema de gestión de paquetes y entornos (Anaconda / Miniconda) que instala paquetes no solo Python, también binarios y dependencias del sistema.
- Útil en ciencia de datos y con paquetes que dependen de bibliotecas nativas (por ejemplo, NumPy o SciPy), porque sus canales suelen ofrecer binarios preconstruidos compatibles entre sí; no elimina toda necesidad de compilación para cualquier paquete.
- Permite crear entornos y exportarlos con `environment.yml`.
- **Ventajas:** crea entornos con una versión concreta de Python y resuelve conjuntamente paquetes Python y dependencias binarias. Puede simplificar instalaciones científicas complejas en plataformas compatibles.
- **Inconvenientes:** requiere instalar conda (Miniconda o Anaconda), consume más espacio y algunos paquetes o versiones pueden no estar en los canales configurados. La disponibilidad y actualización dependen del canal.

Comparación por propósitos:
- **Proyecto web o aplicación con dependencias Python comunes** (por ejemplo, Flask y `requests`): `venv` + `pip` suele ser la opción más simple y ligera.
- **Biblioteca Python disponible en PyPI con rueda para la plataforma** (por ejemplo, una dependencia pura de Python): `pip install paquete` es directo; no suele hacer falta conda.
- **Análisis de datos con NumPy, SciPy y pandas, especialmente en un equipo donde la instalación de bibliotecas nativas da problemas:** `conda install numpy scipy pandas` puede proporcionar binarios compatibles y evitar configurar compiladores manualmente.
- **Proyecto que necesita fijar también la versión de Python y dependencias no Python:** conda y `environment.yml` permiten describir ese entorno; `requirements.txt` con pip documenta principalmente paquetes instalados con pip.
- **Paquete disponible en PyPI pero no en los canales conda usados:** se puede instalar con `pip` dentro de un entorno conda. Conviene instalar primero conda y después pip, y evitar seguir modificando conda tras instalar con pip, para reducir conflictos del resolvedor.
- **Paquete nativo sin rueda ni binario conda para el sistema:** cualquiera de las opciones podría exigir compilación o pasos específicos de la plataforma; comprueba primero las instrucciones y los binarios disponibles.

En resumen, `pip` es adecuado cuando priman la sencillez y el ecosistema PyPI; `conda` resulta conveniente cuando se necesita coordinar Python con bibliotecas binarias o dependencias externas. No son excluyentes, pero mezclar instaladores requiere cuidado.

Comandos básicos `conda`:

```bash
conda create -n mi_entorno python=3.10
conda activate mi_entorno
conda install numpy pandas scikit-learn
conda env export > environment.yml
conda env create -f environment.yml
```

Instalar con pip dentro de un entorno conda, si el paquete no está en los canales configurados:

```bash
conda activate mi_entorno
python -m pip install nombre-del-paquete
```

## Buenas prácticas
- Mantén un único fichero de dependencias por proyecto (`requirements.txt` o `environment.yml`).
- Usa entornos por proyecto y no la instalación global.
- Para reproducibilidad estricta, fija versiones en el fichero de dependencias.
- Considera `pip-tools` o `poetry` para gestión avanzada de dependencias y bloqueo de versiones.

## Tabla resumen: `pip` y `conda`

| Característica o contexto | `pip` (normalmente con `venv`) | `conda` |
|---|---|---|
| Qué instala | Paquetes Python desde PyPI, incluidos paquetes puros y ruedas binarias disponibles. | Paquetes Python y binarios, además de algunas dependencias externas al ecosistema Python. |
| Gestión del entorno | `venv` crea y aísla el entorno; pip instala sus paquetes. | Crea y administra entornos, incluida la versión de Python. |
| Catálogo | Amplia disponibilidad de paquetes Python en PyPI. | Disponibilidad según los canales configurados; no todos los paquetes de PyPI están allí. |
| Dependencias nativas | Puede requerir ruedas compatibles o compilación y herramientas del sistema. | A menudo ofrece binarios coordinados, lo que puede simplificar dependencias nativas. |
| Ventajas principales | Ligero, estándar y sencillo para proyectos Python convencionales. | Resuelve conjuntamente versiones y dependencias binarias; práctico para ciencia de datos. |
| Inconvenientes principales | No administra por sí solo el intérprete ni todas las bibliotecas del sistema; una instalación puede requerir compilación. | Requiere instalar conda, puede usar más espacio y depende de los paquetes y versiones disponibles en los canales. |
| Ejemplo de uso recomendado | Aplicación web con Flask y `requests`: `python -m venv .venv` y `python -m pip install flask requests`. | Análisis científico con NumPy y SciPy: `conda create -n datos python=3.10 numpy scipy`. |
| Reproducibilidad | `requirements.txt` (para reproducir estrictamente, fija versiones). | `environment.yml` puede describir paquetes, canales y versión de Python. |
| Combinación | No aplica como instalador de entorno; se usa dentro de `venv`. | Se puede usar pip dentro del entorno si falta un paquete en los canales; instala primero con conda y evita mezclar cambios sin necesidad. |
