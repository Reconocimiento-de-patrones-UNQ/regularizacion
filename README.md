# Clase 4 — Regularización y modelos lineales generalizados

**Maestría en Bioinformática y Biología de Sistemas — UNNOBA**  
**Reconocimiento de Patrones en Bioinformática**


En esta sesión unificamos conceptos previos para abordar la **regularización**, la herramienta fundamental para tratar con alta dimensionalidad ($p \\gg n$) cuando el objetivo es la predicción. 

## Estructura del Repositorio

  * [Clase4_Reconocimiento_de_Patrones.ipynb](https://colab.research.google.com/drive/1V7bsRZH28QFgSeCk3gGye93Xq13SWg4n): Notebook con la implementación de modelos lineales sobre el dataset *Breast Cancer Wisconsin*. Incluye simulaciones de inestabilidad y ejercicios de búsqueda de hiperparámetros óptimos.
  * **`bibliografia_clase4.md`**: Compendio de lecturas fundamentales (Hastie, Tibshirani) y videos de StatQuest para visualizar la diferencia geométrica entre penalizaciones.

## Cómo ejecutar el material

### Opción A: Google Colab (Recomendado)

**Abrir el notebook utilizando el enlace citado a continuación para aprovechar el entorno de Google Colab preconfigurado con todas las dependencias necesarias:**  

**[Regularización](https://colab.research.google.com/drive/1V7bsRZH28QFgSeCk3gGye93Xq13SWg4n)**

### Opción B: Ejecución Local

Asegúrate de instalar el stack científico requerido. El escalado de variables es **crítico** para que la regularización sea justa:

``` bash
pip install numpy pandas matplotlib seaborn scikit-learn scipy statsmodels

```
