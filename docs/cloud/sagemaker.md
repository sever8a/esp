--- 
title: AWS Sagemaker
summary: Utiliza los recursos de AWS en la nube.
authors:
    - Revisión autorizada
    - Jose Robledano
date: 2026-07-28
---

# AWS SageMaker: resumen breve

AWS SageMaker es una plataforma gestionada para desarrollar, entrenar y desplegar modelos de machine learning a escala en AWS. Integra servicios que cubren todo el ciclo de vida de ML: notebooks gestionados, preparación y etiquetado de datos, entrenamiento distribuido, ajuste de hiperparámetros, despliegue de endpoints en producción, inferencia batch y pipelines reproducibles.

Principales posibilidades:
- **Notebooks gestionados:** entornos Jupyter listos para usar con acceso a datos en S3 y recursos de cómputo escalables.
- **Entrenamiento:** soporta entrenamiento distribuido en instancias GPU/CPU, con imágenes preconfiguradas o contenedores personalizados.
- **Tuning y AutoML:** ajuste automático de hiperparámetros (Hyperparameter Tuning) y capacidades de SageMaker Autopilot para pipelines automáticos.
- **Despliegue:** endpoints en tiempo real, despliegue en Multi-Model endpoints y endpoint autoscaling; soporte para inferencia en batch y compresión/optimización de modelos (Neo, model compilation).
- **MLOps:** SageMaker Pipelines para orquestar workflows reproducibles, integración con CloudWatch, IAM y CI/CD (CodePipeline, CodeBuild).
- **Etiquetado y procesamiento:** SageMaker Ground Truth para anotación de datos y Processing Jobs para transformaciones a escala.

Uso con AWS Academy:
- AWS Academy ofrece recursos educativos y laboratorios que pueden incluir acceso a servicios como SageMaker dentro de entornos de enseñanza. En un curso de AWS Academy se pueden crear ejercicios prácticos que usan SageMaker Notebooks, entrenamientos y despliegues controlados.
- Consideraciones prácticas: gestionar costes (usar instancias de menor coste o límites temporales), preparar datasets en S3, crear roles IAM con permisos mínimos para estudiantes y usar recursos temporales que se limpien al finalizar las prácticas.
- Recomendación: para docencia usar cuentas de aula/provisionadas por AWS Academy o créditos controlados; proporcionar notebooks con ejemplos y un pipeline sencillo para que el alumnado experimente sin incurrir en costes inesperados.

¿Quieres que añada un ejemplo mínimo de notebook de inicio o un diagrama de flujo para un pipeline simple en `docs/cloud/sagemaker.md`? 
