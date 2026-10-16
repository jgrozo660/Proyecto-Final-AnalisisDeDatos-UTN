# Resultados

Todos los archivos se generan al ejecutar `proyecto_integrador.ipynb` y son los que usa el informe final.

| Archivo | Contenido |
|---|---|
| `eda_calidad.csv` | Nulos, centinela de `TotalCharges`, duplicados |
| `eda_h1_contrato.csv`, `eda_h2_tenure.csv`, `eda_h3_servicios_pago.csv`, `eda_h4_cargo_mensual.csv`, `fig_eda.png` | Evidencia descriptiva de las hipótesis H1-H4 |
| `cv_5folds.csv`, `cv_resumen.csv` | Validación cruzada de 5 folds (5 modelos) |
| `seleccion_modelo.csv` | Regla definida de antemano: umbral de empate, empatados y elegido |
| `model_metrics.csv` | Test interno: ranking aleatorio y 5 modelos (PR-AUC, ROC-AUC, recall y precisión en el 20 % y con umbral 0,5) |
| `intervalos_confianza.csv` | Intervalos de confianza del 95 % del modelo elegido y diferencia contra Gradient Boosting |
| `captura_por_cupo.csv`, `abandonos_por_decil.csv`, `fig_pr_ganancia.png` | Abandonos detectados según el cupo (10-50 %), por tramos de 10 %, curvas PR y de ganancia |
| `fig_probabilidades.png`, `umbral_f1.csv` | Probabilidades predichas contra tasas reales y umbral Sí/No elegido con la validación cruzada |
| `matriz_confusion.csv`, `reporte_clasificacion.csv`, `fig_roc.png` | Matriz de confusión, precisión/recall/F1 por clase y curva ROC |
| `shap_global.csv`, `shap_direccion.csv`, `fig_shap_global.png` | SHAP global y dirección del efecto por categoría |
| `shap_local_case.csv`, `fig_shap_local.png` | SHAP local de un cliente real del top 20 % |
| `quitar_variables.csv` | Prueba de quitar cada grupo de variables (H1-H4) |
| `auditoria_grupos.csv`, `auditoria_grupos_validacion_cruzada.csv`, `brecha_genero_ic.csv`, `sin_atributos_sensibles.csv` | Auditoría ética por grupos |
| `ciclo_vida_gasto.csv` | Meses activos, tasa de abandono y cargo mensual por tipo de contrato |
| `segmentos_valor_riesgo.csv` | Segmentos Golden, Champions, En riesgo de bajo valor y Estables de bajo valor |
| `retener_vs_adquirir.csv` | Retener a los Golden frente a reemplazarlos con clientes nuevos (CAC genérico USD 300) |
| `valor_cliente_escenarios.csv` | Valor neto preservado según el costo por cliente retenido (USD 100, 1.000, 10.000), al azar, por riesgo y por valor en riesgo |
| `predicciones_test.csv`, `submission.csv` | Predicciones sobre data/test.csv |
| `resumen.csv` | Números principales |
