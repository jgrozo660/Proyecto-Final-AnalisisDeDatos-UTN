# Datos

- Fuente: competencia de Kaggle *Predicción de fuga de cliente* (telecomunicaciones), basada en el dataset Telco Customer Churn.
  https://www.kaggle.com/competitions/prediccion-de-fuga-de-cliente/data
- `train.csv`: 5.634 clientes, 21 columnas (incluye la variable objetivo `Churn`).
- `test.csv`: 1.409 clientes, 20 columnas (sin `Churn`; solo para generar predicciones).

Ambos archivos se incluyen en esta carpeta para que el notebook se ejecute sin pasos extra; el notebook valida su forma al cargarlos.

**Nota de calidad:** el archivo viene pre-imputado. Los clientes con `tenure = 0` tienen `TotalCharges = 1397,475` (la mediana); el notebook lo corrige a 0. Ver `data_log.md`.

## Diccionario de variables

| Variable | Tipo | Descripción |
|---|---|---|
| `customerID` | Identificador | Código del cliente (no se usa para modelar) |
| `gender` | Categórica | Género del cliente (Female / Male) |
| `SeniorCitizen` | Binaria | 1 si es adulto mayor |
| `Partner`, `Dependents` | Categórica | Si tiene pareja / personas a cargo |
| `tenure` | Numérica | Antigüedad en meses (0-72) |
| `PhoneService`, `MultipleLines` | Categórica | Servicio telefónico y líneas múltiples |
| `InternetService` | Categórica | DSL, fibra óptica o sin internet |
| `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport` | Categórica | Servicios adicionales de soporte y seguridad |
| `StreamingTV`, `StreamingMovies` | Categórica | Servicios de streaming |
| `Contract` | Categórica | Mes a mes, un año o dos años |
| `PaperlessBilling` | Categórica | Facturación electrónica |
| `PaymentMethod` | Categórica | Electronic check, Mailed check, transferencia automática o tarjeta automática |
| `MonthlyCharges` | Numérica | Cargo mensual (18,40 - 118,75) |
| `TotalCharges` | Numérica | Cargo total acumulado |
| `Churn` | Objetivo | Yes si el cliente abandonó (solo en `train.csv`) |
