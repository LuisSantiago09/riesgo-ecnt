# Predicción del riesgo de ECNT asociado a determinantes sociales — Fase 2 (Desarrollo y Modelado)

**Grupo 05** · Diego Nieves, Harold Solano, Luis Vivanco

Modelos de regresión supervisada (regresión múltiple, Ridge, Random Forest y Gradient Boosting) para estimar un
índice municipal de riesgo de enfermedades crónicas no transmisibles (ECNT) a partir de los determinantes sociales
agua, saneamiento y educación (NBI, Censo 2018) en los 197 municipios del Caribe colombiano.

> ## Variable objetivo simulada
> `ir_ecnt_sim` (0–100) se **genera de forma sintética** con un proceso explícito
> (`src/ecnt/target_simulation.py`). Las métricas miden qué tan bien cada algoritmo recupera esa señal conocida;
> **no son evidencia de riesgo clínico real**. Para pasar a datos reales, reemplace esa columna (ver `config.TARGET`).

## Resultados (resumen)

| Modelo | RMSE CV anidada (197 mpios.) | RMSE test (n = 40) | R² test |
|---|---|---|---|
| Media (referencia) | – | 10,20 | 0,000 |
| Regresión múltiple (baseline) | 5,61 ± 1,21 | 4,77 | 0,781 |
| Regresión múltiple + ing. de características | 4,08 ± 0,56 | 4,34 | 0,819 |
| Ridge | 4,00 ± 0,45 | 4,15 | 0,834 |
| Random Forest | 4,02 ± 0,45 | 4,19 | 0,832 |
| **Gradient Boosting (propuesto)** | **3,83 ± 0,45** | **4,02** | **0,844** |

Detalle, figuras y discusión: `docs/Documento_Tecnico_Fase2.docx` y `reports/`.

## Estructura

data/raw/            Libro Excel original (NBI + microdatos Cesar)
data/processed/      datos_modelado.csv y particiones train/val/test (generados)
src/ecnt/            Paquete: config, data_loading, target_simulation, features, models, evaluation
scripts/             01_preparar_datos.py · 02_entrenar_modelos.py · 03_evaluar.py
tests/               Pruebas del pipeline (carga, objetivo, características, sin fuga)
reports/figures/     Figuras 1–7
reports/metrics/     Tablas de resultados (CSV/JSON) y logs
models/              Modelos entrenados (.joblib, no versionados)
docs/                Documento técnico 

## Cómo ejecutar

bash
python -m venv .venv && source .venv/bin/activate     # Windows: .venv\Scripts\activate
pip install -r requirements.txt
./run_all.sh            # o ejecutar los tres scripts en orden
python tests/test_pipeline.py   # o: pytest -q

## Decisiones metodológicas

- Partición =  60/20/20 estratificada por quintiles del objetivo (117/40/40). El test se usa una sola vez.
- **Sin fuga de información:** se excluyen `servicios_alto`, `educacion_alto`, `segmento` (derivadas del NBI) y los
  microdatos del Cesar (87 % de nulos estructurales); imputación, escalado y codificación se ajustan solo con
  entrenamiento (dentro de `sklearn.Pipeline`).
- **Ajuste de hiperparámetros:** `RandomizedSearchCV` con CV repetida 5×2 sobre entrenamiento.
- **Evaluación:** RMSE/MAE/R², IC 95 % bootstrap, vista de clasificación (AUC, F1, precisión, recall), CV anidada,
  Wilcoxon pareado, importancia por permutación, residuales, curva de aprendizaje y sensibilidad al ruido.

## Control de versiones

## Fuentes

DANE — Censo Nacional de Población y Vivienda 2018 (NBI por municipio y microdatos del Cesar).

## Integrantes
- Diego Nieves
- Harold Solano
- Luis Vibanco
