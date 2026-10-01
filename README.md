# Optimizador masivo de estrategias · VectorBT + CUDA

Notebook de Google Colab (`optimizador_vectorbt_gpu.ipynb`) que optimiza en la GPU una malla de
cientos de miles de combinaciones (cruce de SMA + filtro RSI) sobre un CSV de Dukascopy. Descarta
automáticamente las estrategias perdedoras, valida el Top en Out-Of-Sample con
`vbt.Portfolio.from_signals()` y exporta las estrategias robustas a Google Drive.

1. Sube el CSV a `MyDrive/activos`.
2. Abre el notebook en Colab con un entorno de GPU.
3. Edita solo la **Celda 2** y ejecuta todo.

Notas técnicas:
- Cada hilo CUDA (Numba) simula una combinación; los indicadores se calculan con CuPy en la VRAM.
- El motor GPU reproduce exactamente a VectorBT (misma ejecución en la apertura de la vela siguiente,
  mismas comisiones); la Celda 4 lo comprueba en cada ejecución.
- Sin GPU, el mismo código se ejecuta con Numba en CPU paralelo.
