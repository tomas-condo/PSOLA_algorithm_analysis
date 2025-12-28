# Trabajo Práctico Especial: Cambios de Velocidad de la Señal de Habla

## Descripción General
Este proyecto aborda el procesamiento digital de señales de voz, enfocándose específicamente en la modificación de la velocidad de reproducción (Time Stretching).

El objetivo principal es analizar y comparar cómo diferentes algoritmos afectan la inteligibilidad y las características espectrales de la voz (frecuencia glótica y posición de los formantes). Se contrastan métodos simples de remuestreo contra métodos más avanzados en el dominio de la frecuencia como el **Phase Vocoder**.

## Metodología y Tareas

El proyecto se divide en la implementación de dos enfoques principales aplicados a las señales de prueba *"Picasso lenta"* y *"Picasso rápida"*.

### 1. Métodos de Remuestreo (Dominio Temporal)
Estos métodos alteran la velocidad de la señal variando la cantidad de muestras, lo que conlleva inevitablemente a un desplazamiento de las características en frecuencia (efecto "ardilla" o "gigante").

* **Diezmado (Aumento de velocidad):**
    * Se procesa la señal *"Picasso lenta"* para aumentar su velocidad al doble.
    * Se implementa quitando puntos de la señal temporal.
    * Incluye un **filtro antialiasing** (diseñado por método de ventaneo) para evitar solapamiento espectral antes del diezmado.
* **Interpolación (Disminución de velocidad):**
    * Se procesa la señal *"Picasso rápida"* para disminuir su velocidad a la mitad.
    * Utiliza técnicas de interpolación para agregar puntos y suavizar la señal resultante.

### 2. Phase Vocoder (Dominio Frecuencial - TFCT)
Este método busca variar la velocidad de la señal preservando sus características en frecuencia (sin desplazar formantes ni armónicos), trabajando sobre la Transformada de Fourier de Corto Tiempo (TFCT).

* **Aumento de velocidad:**
    * Modificación de la matriz de la TFCT de la señal *"Picasso lenta"* eliminando una de cada dos columnas (ventanas temporales).
    * Recuperación de la señal temporal mediante la iTFCT (Transformada Inversa).
* **Disminución de velocidad:**
    * Modificación de la TFCT de la señal *"Picasso rápida"* mediante la interpolación de columnas originales.
    * Reconstrucción de la señal mediante iTFCT.

## Estructura del Proyecto

* **`Script_PSOLA.ipynb`**: Jupyter Notebook que contiene:
    * Carga y preprocesamiento de los audios.
    * Implementación de funciones de diezmado e interpolación.
    * Implementación del algoritmo Phase Vocoder (Análisis, Modificación, Síntesis).
    * Generación de gráficos y **espectrogramas** comparativos para observar los cambios en la energía espectral y formantes.

## Requisitos y Dependencias

Para ejecutar este proyecto se requiere Python 3 y las siguientes librerías científicas:

* `numpy`: Para manipulación de matrices y operaciones matemáticas.
* `scipy`: Para el procesamiento de señales (filtros, lectura de archivos .wav).
* `matplotlib`: Para la generación de gráficos y espectrogramas.

```bash
pip install numpy scipy matplotlib jupyter
