
# Predicción del riesgo de enfermedades crónicas no transmisibles asociadas a determinantes sociales en población dispersa

## 1. Descripción del proyecto

Este proyecto de inteligencia artificial busca explorar la relación entre los determinantes sociales y la prevalencia de hipertensión a nivel municipal, como aproximación al estudio de las desigualdades en salud en población dispersa.

El proyecto contempla el procesamiento de datos, el entrenamiento de modelos de regresión, la evaluación de su desempeño y la comparación de resultados.

**Importante:** la variable objetivo de salud utilizada actualmente es simulada y no corresponde a estadísticas oficiales. Por tanto, los resultados son experimentales y no deben interpretarse como predicciones reales de salud.

## 2. Objetivo general

Construir y evaluar modelos de inteligencia artificial que permitan explorar la relación entre determinantes sociales y la prevalencia de hipertensión a nivel municipal.

## 3. Datos utilizados

El conjunto de datos experimental contiene:

- 2.316 registros de municipio-año.
- 193 municipios.
- Periodo comprendido entre 2012 y 2023.
- Indicadores sociales, demográficos y una variable objetivo de prevalencia de hipertensión simulada.

Entre las variables predictoras se encuentran las necesidades básicas insatisfechas, miseria, componentes de vivienda, agua y saneamiento, hacinamiento, inasistencia educativa y dependencia económica.

## 4. Metodología

El desarrollo se divide en las siguientes etapas:

1. Carga y exploración del conjunto de datos.
2. Limpieza de datos y revisión de valores faltantes y duplicados.
3. Selección de variables predictoras y variable objetivo.
4. División en conjuntos de entrenamiento, validación y prueba por municipio.
5. Entrenamiento de los modelos.
6. Ajuste de hiperparámetros mediante validación cruzada agrupada.
7. Evaluación cuantitativa y comparación de resultados.

## 5. Modelos implementados

### Regresión lineal múltiple

Se utiliza como modelo base para estimar relaciones lineales entre los determinantes sociales y la variable objetivo.

### Gradient Boosting Regressor

Se utiliza como modelo propuesto para explorar relaciones no lineales. Sus hiperparámetros se ajustaron mediante búsqueda de parámetros y validación cruzada agrupada.

## 6. Métricas de evaluación

Se utilizaron las siguientes métricas:

- **MAE:** error absoluto medio.
- **RMSE:** raíz del error cuadrático medio.
- **R²:** coeficiente de determinación.

Para MAE y RMSE, los valores más bajos indican menor error. Para R², los valores más altos indican mayor capacidad explicativa, teniendo en cuenta que un valor bajo refleja un ajuste limitado.

## 7. Resultados en el conjunto de prueba

| Modelo | MAE | RMSE | R² |
|---|---:|---:|---:|
| Regresión lineal múltiple | 1.6955 | 2.0079 | 0.1674 |
| Gradient Boosting ajustado | 1.7538 | 2.1017 | 0.0878 |

En la evaluación realizada, la regresión lineal múltiple obtuvo mejores resultados en las tres métricas. Sin embargo, ambos modelos presentaron valores de R² bajos.

Estos resultados deben interpretarse como una evaluación metodológica preliminar, debido a que la variable objetivo utilizada es simulada.

## 8. Tecnologías utilizadas

- Python
- Google Colab
- pandas
- NumPy
- scikit-learn
- Matplotlib
- Seaborn

## 9. Estructura del repositorio

```text
prediccion-ecnt-determinantes-sociales/
├── notebooks/
│   └── modelo_prediccion_ecnt.ipynb
├── resultados/
│   ├── comparacion_modelos.csv
│   └── valores_reales_vs_predichos.png
├── README.md
├── requirements.txt
└── .gitignore
```

Los nombres de los archivos mostrados son una estructura de referencia. Deben coincidir con los archivos que realmente estén incluidos en el repositorio.

## 10. Cómo ejecutar el proyecto

### Opción A: Google Colab

1. Abrir el notebook ubicado en la carpeta `notebooks/`.
2. Cargar el archivo CSV del conjunto de datos.
3. Ejecutar las celdas en orden.
4. Revisar las métricas, las comparaciones y las gráficas generadas.

### Opción B: Entorno local

1. Instalar Python.
2. Instalar las dependencias:

```bash
pip install -r requirements.txt
```

3. Abrir y ejecutar el notebook con Jupyter Notebook o JupyterLab.
4. Asegurarse de que el archivo de datos esté disponible en la ruta utilizada por el notebook.

## 11. Limitaciones y trabajo futuro

- La variable objetivo de salud es simulada y no oficial.
- Algunos indicadores sociales con demasiados valores faltantes fueron excluidos.
- Algunos indicadores sociales se repiten entre años y no reflejan necesariamente cambios anuales reales.
- Los modelos presentan capacidad explicativa limitada según los valores de R².

Como trabajo futuro, se propone incorporar datos oficiales de salud, revisar la calidad y cobertura de las variables y volver a entrenar y evaluar los modelos con información real.

## 12. Estado del proyecto

Proyecto en desarrollo académico. Se ha implementado el flujo experimental de preprocesamiento, entrenamiento, ajuste y evaluación de dos modelos de regresión.

Los resultados actuales no constituyen una herramienta clínica ni una estimación validada del riesgo real de enfermedad.
