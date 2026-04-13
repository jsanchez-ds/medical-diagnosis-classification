# Datos

## Fuente

Wisconsin Breast Cancer Diagnostic Dataset (WBCD).
Disponible en [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Breast+Cancer+Wisconsin+(Diagnostic))
y en [Kaggle](https://www.kaggle.com/datasets/uciml/breast-cancer-wisconsin-data).

## Esquema

| Columna | Descripcion |
|---------|-------------|
| `id` | Identificador unico del paciente |
| `diagnosis` | Diagnostico: M = maligno, B = benigno |
| `radius_mean` | Media de distancias del centro al perimetro |
| `texture_mean` | Desviacion estandar de valores en escala de grises |
| `perimeter_mean` | Perimetro medio del nucleo |
| `area_mean` | Area media del nucleo |
| `smoothness_mean` | Variacion local en las longitudes del radio |
| `compactness_mean` | (perimetro^2 / area) - 1.0 |
| `concavity_mean` | Severidad de porciones concavas del contorno |
| `concave points_mean` | Numero de porciones concavas del contorno |
| `symmetry_mean` | Simetria del nucleo |
| `fractal_dimension_mean` | Aproximacion de la dimension fractal |
| `*_se` | Error estandar de cada metrica |
| `*_worst` | Peor valor (media de los 3 mayores) de cada metrica |
| `Unnamed: 32` | Columna vacia (se elimina en el analisis) |

Las 30 variables numericas se calculan para cada imagen a partir de 10 caracteristicas
base (mean, se, worst).
