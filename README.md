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

├── notebooks/
│   ├── limpieza_seleccion_dataicfes.ipynb   # Fase obligatoria: limpieza, filtros regionales e ingeniería de datos
│   ├── regression_lineal_multiple_M.ipynb   # Modelo 1: Regresión Lineal Regularizada (Ridge)
│   ├── Random_forest.ipynb                  # Modelo 2: Ensamble paralelo (Random Forest)
│   └── gradient_boosting_m.ipynb            # Modelo 3: Ensamble secuencial (HistGradientBoosting)
├── requirements.txt                         # Dependencias y librerías del proyecto
└── README.md                                # Documentación del repositorio

### Descripción de los Notebooks

1. **`limpieza_seleccion_dataicfes.ipynb` (Fase previa indispensable):**  
   * Consolidación de 14 aplicaciones históricas (2019-1 a 2025-2).
   * Filtrado geográfico de cohortes en Bogotá D.C. (código DANE `11`) y Cundinamarca (código DANE `25`).
   * Depuración de valores nulos en el objetivo (`punt_global`), cálculo de `estu_edad` y control demográfico ($10 \le \text{edad} \le 80$).
   * Mitigación de fuga de información (*target leakage*) descartando niveles de desempeño y subpuntajes por área.
   * Construcción de variables compuestas: `indice_bienes` e `indice_consumo`.
   * Exportación del dataset procesado para el modelado.

2. **Modelos predictivos (Ejecución independiente tras la limpieza):**  
   * **`regression_lineal_multiple_M.ipynb`:** Ajuste de línea base lineal regularizada ($L_2$ - Ridge), análisis de supuestos y coeficientes estandarizados.
   * **`Random_forest.ipynb`:** Ajuste de ensamble de árboles en paralelo (*bagging*) y evaluación de importancia intrínseca (*Mean Decrease in Impurity*).
   * **`gradient_boosting_m.ipynb`:** Ajuste de ensamble secuencial optimizado (*boosting* por histogramas), análisis de importancia por permutación (*permutation feature importance*) y diagnóstico de distribución de residuos.

---

## Resumen Comparativo de Métricas de Rendimiento

Los modelos fueron entrenados y evaluados bajo un esquema de partición estratificada 80 % entrenamiento ($n \approx 688.800$) y 20 % prueba independiente ($n \approx 172.200$) con semilla fija (`random_state=42`):

| Model | R2 (Train) | R2 (Test) | RMSE (Test) | MAE (Test) |
| :--- | :---: | :---: | :---: | :---: |
| **Ridge Regression** | 0.3638 | 0.3627 | 39.97 | 32.14 |
| **Random Forest** | 0.3811 | 0.3639 | 39.93 | 32.31 |
| **HistGradientBoosting** | **0.4534** | **0.4276** | **37.88** | **30.39** |

* El estimador **HistGradientBoosting** obtuvo el mejor rendimiento global, alcanzando un $R^2 = 0.4276$ en prueba y reduciendo el error cuadrático medio ($\text{RMSE} = 37.88$) y el error absoluto medio ($\text{MAE} = 30.39$).
* La diferencia entre el ajuste de entrenamiento y prueba ($\Delta R^2 = 0.0258$) valida la ausencia de sobreajuste (*overfitting*) en el modelo ganador.
* El diagnóstico residual reportó un sesgo medio prácticamente nulo ($-0.14$ puntos en la escala de 0 a 500).

---

## Instalación del Entorno de Ejecución

Para reproducir los experimentos localmente, clone el repositorio e instale las dependencias especificadas en `requirements.txt`:

```bash
# 1. Clonar el repositorio
git clone [https://github.com/andresto92/Comparing-Models-to-Predict-Standardized-Test-Scores.git](https://github.com/andresto92/Comparing-Models-to-Predict-Standardized-Test-Scores.git)
cd Comparing-Models-to-Predict-Standardized-Test-Scores

# 2. Crear y activar el entorno virtual
python -m venv venv

# En Linux / macOS:
source venv/bin/activate
# En Windows:
venv\Scripts\activate

# 3. Instalar librerías
pip install --upgrade pip
pip install -r requirements.txt

# 4. Iniciar Jupyter Lab
jupyter lab
