# Datos

- Fuente: competencia de Kaggle *Predicción de fuga de cliente* (telecomunicaciones), basada en el dataset Telco Customer Churn.
  https://www.kaggle.com/competitions/prediccion-de-fuga-de-cliente/data
- `train.csv`: 5.634 clientes, 21 columnas (incluye la variable objetivo `Churn`).
- `test.csv`: 1.409 clientes, 20 columnas (sin `Churn`; solo para generar predicciones).

Ambos archivos se incluyen en esta carpeta (provistos por la cátedra) para que el notebook se ejecute sin pasos extra; el notebook valida su forma al cargarlos.

**Nota de calidad:** el archivo viene pre-imputado. Los clientes con `tenure = 0` tienen `TotalCharges = 1397,475` (la mediana); el notebook lo corrige a 0. Ver `data_log.md`.
