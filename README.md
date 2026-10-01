# Optimizador masivo de estrategias · VectorBT + CUDA

Notebook de Google Colab (`optimizador_vectorbt_gpu.ipynb`) que optimiza en la GPU una malla de
cientos de miles de combinaciones (cruce de SMA + filtro RSI). Descarta automáticamente las
estrategias perdedoras, valida el Top en Out-Of-Sample con `vbt.Portfolio.from_signals()` y
exporta las estrategias robustas a Google Drive.

1. Abre el notebook en Colab con un entorno de GPU.
2. Edita solo la **Celda 2** (instrumento, temporalidad, dirección…) y ejecuta todo.

Datos:
- `FUENTE_DATOS = "DESCARGAR"`: descarga desde Dukascopy (`dukascopy-python`) y guarda en
  `MyDrive/activos/datos_descargados/*.parquet`. Las siguientes ejecuciones solo descargan las
  velas nuevas; la descarga es reanudable si se corta.
- `FUENTE_DATOS = "CSV"`: archivo propio en `MyDrive/activos` (Dukascopy, MetaTrader 4/5,
  genérico, o ticks bid/ask que se agrupan en la temporalidad elegida).

Notas técnicas:
- Cada hilo de un kernel CUDA (compilado con CuPy) simula una combinación; los indicadores se calculan con CuPy en la VRAM.
- El motor GPU reproduce exactamente a VectorBT (misma ejecución en la apertura de la vela siguiente,
  mismas comisiones); la Celda 4 lo comprueba en cada ejecución.
- Sin GPU, la misma lógica se ejecuta con Numba en CPU paralelo.
