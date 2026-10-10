# Resultados

Todos los archivos se generan al ejecutar `proyecto_integrador.ipynb` y son los que usa el informe final.

| Archivo | Contenido |
|---|---|
| `eda_calidad.csv` | Nulos, centinela de `TotalCharges`, duplicados |
| `eda_h1_contrato.csv` … `eda_h4_cargo_mensual.csv`, `fig_eda.png` | Evidencia descriptiva de las hipótesis H1-H4 |
| `cv_5folds.csv`, `cv_resumen.csv` | Validación cruzada de 5 folds (5 modelos) |
| `seleccion_modelo.csv` | Regla ex ante: umbral de empate, empatados y elegido |
| `model_metrics.csv` | Test interno: ranking aleatorio y 5 modelos (PR-AUC, ROC-AUC, @20 %, @0,5, Brier) |
| `bootstrap_ic.csv` | IC 95 % del modelo elegido y diferencia contra Gradient Boosting |
| `captura_por_cupo.csv`, `lift_deciles.csv`, `fig_pr_ganancia.png` | Captura por cupo (10-50 %), lift por deciles, curvas PR y de ganancia |
| `fig_calibracion.png`, `umbral_f1.csv` | Calibración y umbral Sí/No elegido con OOF |
| `shap_global.csv`, `shap_direccion.csv`, `fig_shap_global.png` | SHAP global y dirección del efecto por categoría |
| `shap_local_case.csv`, `fig_shap_local.png` | SHAP local de un cliente real del top 20 % |
| `ablaciones.csv` | Ablaciones de H1-H4 |
| `auditoria_grupos.csv`, `auditoria_grupos_oof.csv`, `brecha_genero_ic.csv`, `sin_atributos_sensibles.csv` | Auditoría ética por grupos |
| `escenario_economico.csv`, `sensibilidad_economica.csv` | Escenario económico paramétrico y sensibilidad |
| `predicciones_test.csv`, `submission.csv` | Predicciones sobre `test.csv` |
| `resumen.csv` | Números principales |
