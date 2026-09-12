# Comparing Machine Learning Models to Predict Standardized Test Scores (Saber 11)

Este repositorio contiene el código fuente, la metodología de preprocesamiento y los modelos de aprendizaje automático desarrollados en el marco del trabajo de investigación para predecir el puntaje global del examen de Estado **ICFES Saber 11** en Bogotá D.C. y Cundinamarca (cohortes 2019–2025), a partir de variables sociodemográficas, económicas, individuales e institucionales.

---

## Autores e Institución
* **Andres Felipe Torres Cequera**
* **Sandra Patricia Barragán Moreno**
* **Eliacid Marcelo Escalante**

**Universidad de Bogotá Jorge Tadeo Lozano**  
Facultad de Ingeniería y Ciencias Básicas  

---

## Fuente de Datos y Acceso

1. **Fuente Oficial Primaria:**  
   Microdatos abiertos del Instituto Colombiano para la Evaluación de la Educación (**ICFES**), disponibles en el repositorio público [DataIcfes](https://www.icfes.gov.co/data-icfes).
2. **Conjunto de Datos Procesado:**  
   Debido al volumen de la muestra consolidada (861.000 observaciones evaluadas a través de 14 cohortes), los archivos preprocesados y matrices intermedias se encuentran alojados en la siguiente carpeta compartida de Google Drive:  
   👉 **[Enlace de descarga - Datos del Proyecto en Google Drive](https://drive.google.com/drive/folders/1WbSlSwUIyEiIYI3k_N5BEvjlE94GXE3F?usp=drive_link)**

---

## Estructura del Repositorio y Flujo de Ejecución

Los cuadernos de trabajo se encuentran organizados dentro de la carpeta `notebooks/`. Para garantizar la trazabilidad metodológica, el flujo de trabajo requiere ejecutar en primer lugar la etapa de preparación de datos; posteriormente, los tres modelos pueden ejecutarse de manera independiente:

```text
Comparing-Models-to-Predict-Standardized-Test-Scores/
├── notebooks/
│   ├── limpieza_seleccion_dataicfes.ipynb   # Fase obligatoria: limpieza, filtros regionales e ingeniería de datos
│   ├── regression_lineal_multiple_M.ipynb   # Modelo 1: Regresión Lineal Regularizada (Ridge)
│   ├── Random_forest.ipynb                  # Modelo 2: Ensamble paralelo (Random Forest)
│   └── gradient_boosting_m.ipynb            # Modelo 3: Ensamble secuencial (HistGradientBoosting)
├── requirements.txt                         # Dependencias y librerías del proyecto
└── README.md                                # Documentación del repositorio
