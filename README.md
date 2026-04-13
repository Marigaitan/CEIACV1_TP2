# Trabajo Práctico N°2 - Visión por Computadora - CEIA

Integrantes: 
- Mariel Gaitán
- Gaspar Rivollier

El trabajo principal se encuentra en [TP2_maxEnf.ipynb](/home/gaspi/CEIACV1_TP2/TP2_maxEnf.ipynb), donde el notebook:

- lee el archivo `focus_video.mov`
- calcula una métrica de calidad de imagen basada en Fourier para cada frame
- compara el análisis sobre el frame completo contra una ROI centrada
- grafica las curvas de enfoque e identifica la región de mejor foco
- prueba `unsharp masking` como etapa de preprocesamiento

## Archivos del Proyecto

- [TP2_maxEnf.ipynb](/home/gaspi/CEIACV1_TP2/TP2_maxEnf.ipynb): notebook principal con el experimento completo
- [focus_video.mov](/home/gaspi/CEIACV1_TP2/focus_video.mov): video de entrada utilizado para el análisis
- [pyproject.toml](/home/gaspi/CEIACV1_TP2/pyproject.toml): metadatos del proyecto y dependencias

### 1. Full Frame

`IQM_FF(img_gris)` calcula la métrica de enfoque utilizando el frame completo en escala de grises.

Flujo de trabajo:

1. Aplicar la transformada de Fourier 2D.
2. Centrar el espectro desplazando las bajas frecuencias.
3. Calcular la magnitud del espectro.
4. Contar cuántos coeficientes superan `max(AF) / 1000`.
5. Normalizar por el tamaño de la imagen.

Esto produce una medida de enfoque `FM`, donde valores más altos indican una imagen más nítida.

### 2. ROI Centrada

`IQM_R(img_gris)` aplica la misma métrica, pero únicamente sobre una región de interés centrada que ocupa el 40% de las dimensiones del frame.

Esto resulta útil cuando la zona importante está cerca del centro y el contenido del fondo puede afectar la medición sobre el frame completo.

## Experimento con Unsharp Masking

El notebook también incluye:

- `unsharp_masking(...)` para agudizar imágenes
- `calcular_fm_con_unsharp(...)` para recalcular la métrica de enfoque luego del realce
- funciones auxiliares para detectar y visualizar frames enfocados

El objetivo es evaluar si el realce de nitidez incrementa la cantidad de frames considerados aceptablemente enfocados bajo el umbral elegido.

## Requisitos

Este proyecto utiliza Python `>=3.12` y las siguientes bibliotecas:

- `numpy`
- `matplotlib`
- `opencv-python`

## Instalación

Si usás `uv`:

```bash
uv sync
```

Si preferís `pip`:

```bash
python -m venv .venv
source .venv/bin/activate
pip install numpy matplotlib opencv-python
```
