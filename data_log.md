# Data log - decisiones del proyecto

| # | Etapa | Decisión | Motivo | Evidencia / consecuencia |
|---|---|---|---|---|
| 1 | Datos | Usar `train.csv` (5.634 filas, con `Churn`) y `test.csv` (1.409 filas, sin `Churn`) de la competencia de Kaggle | Datos públicos de la competencia, con la variable objetivo solo en `train.csv` | El notebook valida forma y columnas al cargar |
| 2 | Negocio | Hablar de **tasa de churn observada en la muestra** (26,5 %), no de tasa mensual | El dataset es una foto estática, sin fechas (devolución del tutor) | Toda la redacción usa este término |
| 3 | Calidad | `TotalCharges = 0` cuando `tenure = 0` | Los 8 clientes con `tenure = 0` traían `TotalCharges = 1397,475`, la mediana de la columna: el archivo venía pre-imputado | La pre-entrega había reportado "0 nulos"; se corrige |
| 4 | Calidad | Conservar los 15 duplicados sin `customerID` | Tienen IDs distintos: son clientes diferentes con el mismo perfil | Sin efecto material |
| 5 | Preparación | Descartar "cargo promedio por mes" (pendiente de la pre-entrega) | `TotalCharges / (tenure × MonthlyCharges)` tiene mediana 1,00: repite `MonthlyCharges` | No se agrega |
| 6 | Preparación | Agregar `n_servicios` (cantidad de servicios adicionales, 0-6) | Resume el "enganche" del cliente (H3) | Aporte pequeño; se mantiene por interpretabilidad |
| 7 | Preparación | `SeniorCitizen` como categórica; One-Hot + escalado dentro del `Pipeline` | Evita fuga: el preprocesamiento se ajusta solo con datos de entrenamiento | Mismo pipeline en CV, test y predicción final |
| 8 | Validación | Holdout estratificado 80/20 (misma semilla que la pre-entrega) + CV estratificada 5 folds sobre el 80 % | El test no participa de la selección | `cv_5folds.csv`, `cv_resumen.csv` |
| 9 | Validación | **No** hay validación temporal | No hay fechas en los datos; no se simula | Se reporta como limitación |
| 10 | Modelado | Comparar logística (balanceada, sin ponderar, + SMOTE), Random Forest y Gradient Boosting | Cada uno responde una pregunta; no se agregan modelos de relleno (devolución del tutor) | `model_metrics.csv` |
| 11 | Modelado | SMOTE dentro de `imblearn.Pipeline` | Así solo se aplica a los datos de entrenamiento de cada fold (devolución del tutor) | No mejora el ranking (PR-AUC CV 0,659, igual que sin SMOTE) |
| 12 | Selección | Regla definida de antemano: empate si PR-AUC media ≥ mejor − 1 desvío; entre empatados, el más simple | Evita elegir por el mejor número del test | Los 5 empatan; se elige logística sin ponderar |
| 13 | Métricas | Recall @ 20 % como KPI de negocio, PR-AUC como métrica técnica principal | Cupo operativo + clase minoritaria (devolución del tutor) | Accuracy solo como referencia |
| 14 | Métricas | Meta definida de antemano: Recall @ 20 % ≥ 55 % (mínimo 50 %); techo teórico 75 % | Fijada antes de correr los modelos de la entrega final | Resultado 53,2 %: cumple el mínimo, no la meta |
| 15 | Evaluación | Intervalos de confianza del 95 % remuestreando el test 2.000 veces | El test tiene ~300 abandonos; diferencias de 1-2 puntos pueden ser ruido | GB vs. logística: diferencia no significativa |
| 16 | Probabilidades | Usar la logística sin ponderar para leer probabilidades | `class_weight` y SMOTE inflan las probabilidades | La balanceada sobreestima el riesgo; la sin ponderar se acerca a las tasas reales |
| 17 | Umbral | Umbral Sí/No = 0,328, el que maximiza F1 en las predicciones de la validación cruzada | No se elige con el test | Recall 72,6 %, precisión 56,7 % en test |
| 18 | Interpretación | SHAP (LinearExplainer) sobre el test, sumando one-hot por variable original | Lectura de negocio | SHAP describe el modelo, no causalidad |
| 19 | Interpretación | Leer `MonthlyCharges` con cautela | Su efecto condicional es negativo porque fibra y streaming ya explican los cargos altos (colinealidad) | H4 no se sostiene por encima de los servicios contratados |
| 20 | Hipótesis | Prueba de quitar cada grupo de variables, sobre el mismo test | Mide el aporte propio de cada bloque | Antigüedad: mayor caída; contrato + antigüedad juntos: −7,6 p.p. de PR-AUC |
| 21 | Ética | Auditar recall por género, edad (SeniorCitizen), pareja y dependientes, en test y en validación cruzada | Atributos sensibles | La brecha por género del test no se repite en la validación cruzada; los clientes con dependientes quedan sub-detectados en ambos |
| 22 | Ética | Evaluar el modelo sin `gender` ni `SeniorCitizen` | Minimización de atributos sensibles | Desempeño igual (PR-AUC 0,664 vs. 0,666): se recomienda quitarlos en producción |
| 23 | Negocio | Valor del cliente = `MonthlyCharges` × 24 meses; retención del 30 %; costo por cliente retenido de USD 100, 1.000 y 10.000 | No hay costos reales de la empresa; se usan valores genéricos | Conviene retener mientras cueste menos que el valor del cliente; priorizar por valor en riesgo preserva más valor que por riesgo o al azar |
| 24 | Entrega | Modelo final reentrenado con todo `train.csv` para predecir `test.csv` | Usa toda la información disponible | `predicciones_test.csv`, `submission.csv` |
| 25 | Negocio | Ciclo de vida de 24 meses, contrastado con los datos (los que abandonaron duraron 18 meses en promedio; los que siguen llevan 38) | Telecomunicaciones: gasto mensual y recurrente | `ciclo_vida_gasto.csv` |
| 26 | Negocio | Segmentación por valor (mitad superior, desde USD 1.706) y riesgo (top 20 %): Golden, Champions, En riesgo de bajo valor, Estables de bajo valor | No todos los clientes se rescatan por igual | Golden: 16 % de la cartera, 70 % de abandono, 49 % del valor perdido |
| 27 | Negocio | CAC genérico de USD 300; retener conviene si valor Golden − costo > valor cliente nuevo − CAC | No hay datos de publicidad de la empresa | Costo máximo para retener un Golden: USD 854 |
