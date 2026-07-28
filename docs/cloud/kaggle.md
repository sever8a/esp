--- 
title: Kaggle
summary: Ecosistema para la propuesta y resolución de competiciones.
authors:
    - Revisión autorizada
    - Jose Robledano
date: 2026-07-28
---

# Qué es Kaggle y cómo usarlo

Kaggle es una plataforma online para ciencia de datos que ofrece: competiciones públicas y privadas, repositorio de datasets, entornos de notebooks en la nube (Kaggle Notebooks), recursos educativos (Kaggle Learn) y una comunidad activa de profesionales y estudiantes. Permite experimentar, aprender y compartir soluciones reproducibles.

## Usos principales
- Participar en competiciones para resolver problemas reales o de aprendizaje.
- Explorar y publicar datasets reutilizables.
- Desarrollar y compartir notebooks reproducibles sin necesitar infraestructura local.
- Colaborar y aprender mediante kernels/notebooks, discusiones y tutoriales.

## Cómo empezar (pasos rápidos)
1. Crea una cuenta en https://www.kaggle.com.
2. Completa tu perfil y acepta las normas de la comunidad.
3. Explora `Datasets`, `Notebooks` y `Competitions` para ver ejemplos y soluciones.

## Herramientas útiles: Kaggle CLI
Instala la utilidad oficial para interactuar desde terminal:

```bash
pip install kaggle
# Configura tu token en ~/.kaggle/kaggle.json (descargar desde tu cuenta Kaggle -> Account -> API)
chmod 600 ~/.kaggle/kaggle.json
```

Comandos comunes:

```bash
# Descargar dataset
kaggle datasets download -d owner/dataset-name

# Descargar archivos de una competición
kaggle competitions download -c competition-name

# Enviar una predicción (formato CSV)
kaggle competitions submit -c competition-name -f submission.csv -m "Mi primer envío"

# Listar competiciones disponibles
kaggle competitions list
```

## Crear competiciones propias — consideraciones y pasos

Nota importante: hay distintos tipos de competiciones y niveles de soporte. Kaggle ofrece competiciones "Hosted" (Kaggle administra infraestructura y la visibilidad pública; normalmente para empresas u organizaciones y puede requerir coordinación con el equipo de Kaggle) y opciones educativas/privadas para cursos y grupos. Si buscas máxima flexibilidad o control total, considera alternativas como CodaLab.

Pasos generales para organizar una competición en Kaggle:

1. Definir el problema y el conjunto de datos
- Decide si será de clasificación, regresión, ranking, segmentación, etc.
- Prepara `train/validation/test` y asegúrate de mantener las etiquetas de test ocultas.
- Revisa y anonimiza datos sensibles; documenta la licencia de uso.

2. Definir la métrica de evaluación y las reglas
- Elige una métrica clara (por ejemplo RMSE, AUC, F1, accuracy). Proporciona un script de evaluación si la métrica no es trivial.
- Define límites de envíos, formato del archivo de envío y reglas de desempate.

3. Preparar recursos y materiales
- Provee un baseline y notebooks de inicio para que los participantes arranquen.
- Crea una página de descripción con objetivos, fechas, premios (si hay) y criterios de elegibilidad.

4. Subir datos y configuración
- En un flujo típico subes los datos preparados y configuras la evaluación (en entornos "Hosted" esto se realiza via el panel de competiciones de Kaggle).

5. Prueba interna y lanzamiento
- Antes del lanzamiento público realiza pruebas con un conjunto de pruebas y asegúrate que la evaluación y las reglas funcionan correctamente.

6. Moderación y soporte durante la competición
- Gestiona el foro, responde preguntas frecuentes, publica FAQs y actualizaciones. Mantén transparencia sobre cambios.

7. Cierre y análisis post-competición
- Publica soluciones ganadoras, escribe un post-mortem con lecciones aprendidas y publica los datos (si corresponde) con la licencia adecuada.

Checklist técnico y de seguridad
- Evita fugas de información entre train/test.
- Establece límites de tamaño de envío y límites de tiempo, si procede.
- Proporciona un set de validación pública y un set de evaluación privada para evitar overfitting al leaderboard.

## Ejemplo mínimo de script de evaluación (Python)

```python
import numpy as np
from sklearn.metrics import mean_squared_error

def rmse(y_true, y_pred):
    return np.sqrt(mean_squared_error(y_true, y_pred))

# Uso: cargar arrays y calcular
# y_true = np.loadtxt('test_labels.csv', delimiter=',')
# y_pred = np.loadtxt('submission.csv', delimiter=',')
# print(rmse(y_true, y_pred))
```

## Recursos y referencias
- Documentación oficial de Kaggle: https://www.kaggle.com/docs
- Guía para organizar competiciones (contactar con Kaggle para competiciones Hosted): https://www.kaggle.com/docs/competitions
- Alternativa open-source para competiciones: CodaLab — https://codalab.lisn.upsaclay.fr/

Si quieres, puedo: añadir una plantilla de `README.md` para organizadores, generar un ejemplo de estructura de datos (`train/` `test/` `baseline/`) o preparar un `notebook` inicial con un baseline simple para incluir en la competición.
