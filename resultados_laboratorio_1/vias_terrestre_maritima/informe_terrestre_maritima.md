# Entrega final — vías terrestre y marítima

Las dos series se agregaron por mes y se evaluaron con una división cronológica de 70% para entrenamiento y 30% para prueba. Se compararon ARIMA/SARIMA, Prophet, Holt-Winters, suavizamiento exponencial simple y seasonal naïve. La selección final prioriza el RMSE de prueba entre los modelos con residuos sin autocorrelación significativa al 5%; si ningún modelo cumple ese criterio, se reporta el menor RMSE con la advertencia correspondiente. AIC y BIC solo se contrastan entre candidatos ARIMA/SARIMA.

## Comparación y selección

| Serie | Inicio–fin | ADF p (`log1p`) | d propuesto | Fuerza estacional | Caída 2020 vs 2019 | Modelo final | MAE | RMSE | Ljung-Box p |
|---|---|---:|---:|---:|---:|---|---:|---:|---:|
| Vía terrestre | 2009-01 a 2026-06 | 0.0304 | 0 | 0.177 | -73.6% | Holt-Winters | 143,667 | 158,576 | 0.1099 |
| Vía marítima | 2009-01 a 2026-06 | 0.3033 | 1 | 0.356 | -67.9% | Holt-Winters | 903 | 1,685 | 0.0020 |

## Lectura de las series

- **Vía terrestre:** la ADF aplicada a `log1p` tiene p = 0.0304; por ello no exige diferenciación regular como punto de partida. La descomposición y los gráficos ACF/PACF muestran la estructura anual que se consideró al probar componentes estacionales de período 12. El modelo seleccionado fue **Holt-Winters**, con MAE = 143,667, RMSE = 158,576 y p = 0.1099 en Ljung-Box.
- **Vía marítima:** la ADF aplicada a `log1p` tiene p = 0.3033; por ello requiere evaluar una diferenciación regular como punto de partida. La descomposición y los gráficos ACF/PACF muestran la estructura anual que se consideró al probar componentes estacionales de período 12. El modelo seleccionado fue **Holt-Winters**, con MAE = 903, RMSE = 1,685 y p = 0.0020 en Ljung-Box.

## Residuos y uso de los resultados

Las tablas `comparacion_metricas.csv` y `comparacion_residuos.csv` reúnen las métricas y los diagnósticos de todos los métodos; `residuos_modelos_seleccionados.csv` conserva los residuos punto a punto de los modelos finales. Para la vía marítima, ningún método alcanzó p ≥ 0.05 en Ljung-Box; por eso Holt-Winters se mantiene por su menor RMSE, pero sus residuos muestran autocorrelación y el resultado debe usarse con cautela. La prueba concentra la recuperación posterior a la pandemia y atraviesa el cambio metodológico de 2023, por lo que sirve para comparar métodos bajo un escenario exigente y los modelos deben actualizarse con cada nuevo mes.
