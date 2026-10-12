# Proyecto Final Integrador - Predicción de abandono (churn) de clientes

> **Diplomado en Ciencia de Datos y Análisis Avanzado (UTN.BA) - Unidad 10 - Proyecto Final Integrador**
> **Grupo 4** - Integrantes: Agustín Bilche Braga, Agustina Díaz, Carlos Grozo, Milagros Crespo, Luana Zalcman.

Una empresa de telecomunicaciones pierde a cerca de **1 de cada 4 clientes** de su cartera (tasa de churn observada en la muestra: 26,5 %). El área de Retención puede contactar aproximadamente al **20 % de la cartera** por campaña. El proyecto construye un **ranking de riesgo de abandono** para que ese cupo se use primero con los clientes más propensos a irse.

[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jgrozo660/Proyecto-Final-AnalisisDeDatos-UTN/blob/main/proyecto_integrador.ipynb)

## Entregables

| Recurso | Archivo |
|---|---|
| Informe Final escrito | [`docs/Informe_Final_Proyecto_Integrador.pdf`](docs/Informe_Final_Proyecto_Integrador.pdf) |
| Presentación Final (12 diapositivas) | [`docs/Presentacion_Final_Proyecto_Integrador.pdf`](docs/Presentacion_Final_Proyecto_Integrador.pdf) (editable: `.pptx`) |
| Código Python | [`proyecto_integrador.ipynb`](proyecto_integrador.ipynb) - también en [Google Colab](https://colab.research.google.com/github/jgrozo660/Proyecto-Final-AnalisisDeDatos-UTN/blob/main/proyecto_integrador.ipynb) |
| Pre-entrega | [`docs/Pre-entrega_Proyecto_Final_Integrador.pdf`](docs/Pre-entrega_Proyecto_Final_Integrador.pdf) |
| Predicciones sobre `test.csv` | [`results/predicciones_test.csv`](results/predicciones_test.csv) y [`results/submission.csv`](results/submission.csv) |

## Resultado principal

Todos los números salen de `proyecto_integrador.ipynb` y se guardan en `results/`.

| Métrica (test interno, 1.127 clientes) | Contacto al azar | Modelo elegido (Regresión Logística) |
|---|---:|---:|
| **Abandonos detectados contactando al 20 % de mayor riesgo** | 20,1 % | **53,2 %** (IC 95 %: 49,2 % - 57,9 %) |
| Precisión dentro del 20 % contactado | 26,6 % | 70,4 % |
| PR-AUC (piso = tasa de churn 0,265) | 0,270 | 0,666 |
| ROC-AUC | 0,500 | 0,848 |

Contactando al 20 % mejor rankeado se detecta **2,65 veces** más abandonos que al azar. El techo teórico es 75 % (con una tasa de 26,5 %, un 20 % de contactos no alcanza para cubrir a todos). La meta definida antes de entrenar era 55 %, con un mínimo aceptable de 50 %: **se supera el mínimo pero no la meta**.

### Cómo se eligió el modelo

Se compararon la Regresión Logística de la pre-entrega (balanceada), la logística sin ponderar, la logística con SMOTE aplicado solo en entrenamiento, Random Forest y Gradient Boosting, con validación cruzada de 5 folds. **Los cinco quedan empatados** (todos dentro de un desvío de la mejor PR-AUC, 0,659). La regla fijada antes de mirar el test elige el más simple: **Regresión Logística sin ponderar**, que además da las probabilidades más realistas.

En el test, Gradient Boosting obtiene una PR-AUC apenas mayor (0,673 vs. 0,666), pero la diferencia no es significativa (intervalo de confianza del 95 % de la diferencia: -0,034 a +0,018). Los modelos de árboles no aportan señal adicional en este dataset.

### Qué explica el riesgo

- **Antigüedad** (`tenure`) es la variable más influyente: los primeros meses concentran el abandono (52 % en los primeros 6 meses).
- **Contrato mes a mes**, **fibra óptica** y la **falta de servicios de soporte** (TechSupport, OnlineSecurity) empujan el riesgo hacia arriba.
- Contrato y antigüedad cuentan una historia muy parecida: quitar cualquiera de los dos por separado casi no cambia el desempeño, pero quitarlos juntos baja la PR-AUC 7,6 puntos.

### Recomendación

Usar el ranking como **herramienta de priorización con intervención humana**, empezar con un **piloto A/B** (20 % priorizado por el modelo vs. 20 % al azar) para medir la tasa real de retención, y monitorear el recall por grupo (en particular, los clientes con dependientes quedan sub-detectados).

## Cambios respecto de la pre-entrega (devolución del tutor)

| Devolución | Cómo se resolvió |
|---|---|
| "Tasa de churn mensual" no corresponde: el dataset es estático | Se habla de **tasa de churn observada en la muestra** |
| Comparar el baseline con Random Forest o Gradient Boosting, sin agregar modelos por agregar | Se comparan ambos; cada modelo responde una pregunta concreta |
| Incorporar PR-AUC | PR-AUC es la métrica técnica principal, con su piso explícito |
| Traducir a negocio: contactando al 20 % de mayor riesgo, ¿qué % de abandonos se detecta? | **53,2 %**, con curva de ganancia y tabla por cupo |
| Si se usa SMOTE, solo sobre entrenamiento | SMOTE vive dentro de un `imblearn.Pipeline`: solo ve el fold de entrenamiento. No mejora el ranking |

## Estructura del repositorio

```text
.
├── README.md
├── proyecto_integrador.ipynb      # notebook ejecutado de punta a punta, con salidas
├── requirements.txt
├── data_log.md                    # registro de decisiones y límites
├── .gitignore
├── data/
│   ├── README.md                  # fuente y nota de calidad
│   ├── train.csv
│   └── test.csv
├── results/                       # tablas, figuras y predicciones usadas en el informe
│   └── README.md
└── docs/
    ├── Pre-entrega_Proyecto_Final_Integrador.pdf
    ├── Informe_Final_Proyecto_Integrador.pdf
    ├── Presentacion_Final_Proyecto_Integrador.pdf
    └── Presentacion_Final_Proyecto_Integrador.pptx
```

## Cómo ejecutar el código

**Opción 1 - Google Colab (sin instalar nada):** abrir el notebook con el botón *Open in Colab* de arriba y ejecutar *Entorno de ejecución → Ejecutar todas*. La primera celda clona este repositorio para obtener los datos e instala las librerías que falten.

**Opción 2 - Local:**

```bash
git clone https://github.com/jgrozo660/Proyecto-Final-AnalisisDeDatos-UTN
cd Proyecto-Final-AnalisisDeDatos-UTN
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute --inplace proyecto_integrador.ipynb
```

También puede abrirse con `jupyter notebook proyecto_integrador.ipynb` y ejecutar todas las celdas. Requiere Python 3.10 o superior. Semilla fija (`random_state=42`); la ejecución completa tarda alrededor de un minuto y regenera todo el contenido de `results/`.
