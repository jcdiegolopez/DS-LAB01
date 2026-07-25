# Entrega final — serie total mensual y vía aérea

Las dos series se agregaron mensualmente, cubren el mismo intervalo y se dividieron cronológicamente en 70% entrenamiento y 30% prueba. El total es la serie obligatoria solicitada; no se eliminaron valores atípicos de registros individuales porque corresponden a flujos posiblemente reales.

## Resultados de diagnóstico y selección

| Serie | Inicio–fin | ADF p (`log1p`) | d propuesto | Fuerza estacional | Caída 2020 vs 2019 | Modelo final | MAE | RMSE | Ljung-Box p |
|---|---|---:|---:|---:|---:|---|---:|---:|---:|
| Total mensual | 2009-01 a 2026-06 | 0.0259 | 0 | 0.235 | -73.0% | Holt-Winters | 188,112 | 205,438 | 0.7521 |
| Vía aérea | 2009-01 a 2026-06 | 0.0142 | 0 | 0.159 | -72.3% | ARIMA/SARIMA seleccionado (ARIMA(1, 0, 1)) | 24,962 | 30,140 | 0.5283 |

## Interpretación

- **Total mensual:** la ADF sobre `log1p` tiene p = 0.0259; por ello no requiere diferenciación regular según ADF. La ACF/PACF, la descomposición y los candidatos ARIMA/SARIMA quedan documentados en las figuras y tablas. El modelo final es **Holt-Winters**, con MAE = 188,112 y RMSE = 205,438 en el 30% final.
- **Vía aérea:** la ADF sobre `log1p` tiene p = 0.0142; por ello no requiere diferenciación regular según ADF. La ACF/PACF, la descomposición y los candidatos ARIMA/SARIMA quedan documentados en las figuras y tablas. El modelo final es **ARIMA/SARIMA seleccionado** (ARIMA(1, 0, 1)), con MAE = 24,962 y RMSE = 30,140 en el 30% final.

## Nota de interpretación

El período de prueba incluye la recuperación posterior a la pandemia y el cambio metodológico de 2023. Por eso las métricas son una comparación reproducible entre modelos bajo una prueba exigente, pero los pronósticos operativos deben actualizarse periódicamente y revisarse ante cambios metodológicos.
