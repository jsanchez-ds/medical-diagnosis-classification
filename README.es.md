🌐 [English](README.md) · **Español**

# Clasificación de Diagnóstico Médico — Detección de Cáncer de Mama

Clasificación binaria sobre el dataset **Wisconsin Breast Cancer** (569 registros, 30 features) para distinguir tumores malignos de benignos. El análisis compara **SVM**, **Decision Tree** y **Naive Bayes** bajo dos estrategias de desbalance de clases (under-sampling y over-sampling), con tuning de hiperparámetros vía GridSearchCV y cross-validation de 5-folds.

[![Render Notebook](https://github.com/jsanchez-ds/medical-diagnosis-classification/actions/workflows/render.yml/badge.svg)](https://github.com/jsanchez-ds/medical-diagnosis-classification/actions/workflows/render.yml)
[![View Report](https://img.shields.io/badge/Ver_Reporte-GitHub_Pages-2ea44f?logo=github)](https://jsanchez-ds.github.io/medical-diagnosis-classification/)
![Python](https://img.shields.io/badge/Python-3.11-3776AB?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-SVM%20%7C%20DT%20%7C%20NB-F7931E?logo=scikitlearn&logoColor=white)

> **[→ Lee el reporte completo renderizado](https://jsanchez-ds.github.io/medical-diagnosis-classification/)** — cada gráfico, tabla y output del modelo, sin requerir instalación.

---

## Pregunta de investigación

> ¿Podemos clasificar confiablemente tumores de mama como malignos o benignos usando mediciones de núcleo celular obtenidas de aspirados con aguja fina, y qué tan sensibles son los resultados a la estrategia de corrección de desbalance de clases?

---

## Dataset

El dataset **Wisconsin Diagnostic Breast Cancer (WDBC)** contiene 569 observaciones con 30 features de valor real computados desde imágenes digitalizadas de aspirados con aguja fina. Cada feature describe características de los núcleos celulares (radio, textura, perímetro, área, smoothness, compactness, concavity, concave points, simetría, dimensión fractal) con estadísticos de media, error estándar y peor-caso.

- **357 benignos** (62.7%) / **212 malignos** (37.3%)
- Fuente: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Breast+Cancer+Wisconsin+(Diagnostic))

---

## Metodología

### 1. EDA
- Estadísticos descriptivos y check de valores faltantes
- Heatmap de correlación → selección de features (dropea 14 features muy correlacionados)
- Análisis de distribución de clases

### 2. Preprocesamiento
- Normalización MinMaxScaler a [0, 1]
- Split train/test (80/20, estratificado)

### 3. Manejo de desbalance de clases
| Estrategia | Enfoque | Efecto |
|---|---|---|
| **Under-sampling** | `RandomUnderSampler` | Reduce clase mayoritaria para igualar a la minoritaria |
| **Over-sampling** | `RandomOverSampler` | Duplica clase minoritaria para igualar a la mayoritaria |

### 4. Modelos (GridSearchCV + 5-fold CV)
| Modelo | CV con Under-sampling | CV con Over-sampling |
|---|---|---|
| **SVM** | **97.6%** | **98.1%** |
| Decision Tree | 92.9% | 93.7% |
| Naive Bayes | 92.0% | 92.7% |

### 5. Evaluación
- Curvas ROC y scores AUC (SVM AUC: 0.992 / 0.996)
- Matrices de confusión sobre test hold-out
- Reportes de clasificación (precision, recall, F1)

---

## Hallazgos principales

1. **SVM domina** en ambas estrategias de desbalance con 97% de accuracy test y AUC > 0.99.
2. **Over-sampling supera ligeramente al under-sampling** — preservar toda la información de la clase mayoritaria da generalización marginalmente mejor.
3. **La selección de features por correlación** redujo la dimensionalidad de 30 a 16 features sin pérdida de desempeño.
4. **Decision Tree y Naive Bayes** alcanzan ~93% de accuracy pero son sustancialmente menos robustos que SVM en este dataset.

---

## Stack técnico

`Python` `scikit-learn` `imbalanced-learn` `XGBoost` `seaborn` `matplotlib` `pandas`

---

## Estructura del proyecto

```
medical-diagnosis-classification/
├── README.md
├── analysis.ipynb                  # Notebook de análisis completo
├── data/
│   ├── README.md                   # Referencia de schema
│   └── data.csv                    # Dataset Wisconsin WDBC (569 filas)
└── .github/workflows/
    └── render.yml                  # CI: ejecuta notebook → HTML → Pages
```

---

## Cómo reproducir

### Opción A — Lee el reporte renderizado (sin instalar nada)

Abre <https://jsanchez-ds.github.io/medical-diagnosis-classification/>. El CI re-ejecuta y re-renderiza el notebook en cada push a `main`.

### Opción B — Correr localmente

```bash
pip install pandas numpy scikit-learn matplotlib seaborn xgboost imbalanced-learn jupyter
jupyter notebook analysis.ipynb
```

---

## Autor

**Jonathan Sánchez**
- GitHub: [@jsanchez-ds](https://github.com/jsanchez-ds)
- Universidad de Chile — Ingeniería Civil Industrial
