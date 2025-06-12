# 🧮 Curso de NumPy: Análisis Numérico Eficiente con Python

## 📌 Módulo 1: Conociendo NumPy

### 🔍 ¿Qué es NumPy?
**NumPy (Numerical Python)** es una biblioteca fundamental para la computación científica en Python.  
Permite realizar operaciones matemáticas y estadísticas de manera eficiente con grandes cantidades de datos.

### 🎯 ¿Para qué sirve NumPy?
NumPy facilita el manejo de datos mediante su estructura principal, los **arrays**, y permite ejecutar múltiples operaciones matemáticas y estadísticas con rapidez y eficiencia.

| ⚡ Funcionalidad | 🔍 Descripción |
|----------------|--------------|
| 📊 **Arrays** | Son estructuras tipo tabla o matriz que almacenan datos homogéneos (del mismo tipo). Son más rápidos y eficientes que las listas de Python. |
| ➕ **Operaciones matemáticas** | Permite realizar sumas, restas, multiplicaciones, divisiones y cálculos estadísticos como promedio, desviación estándar y varianza. |
| 🔢 **Álgebra lineal** | Facilita operaciones como multiplicación de matrices, resolución de sistemas de ecuaciones y cálculo de autovalores/autovectores. |
| 🔄 **Transformación de datos** | Ofrece herramientas para modificar estructuras de datos, extraer subconjuntos y combinar múltiples arrays. |

### 🏆 Ventajas de los Arrays de NumPy
✅ Mayor velocidad en operaciones matemáticas  
✅ Menor uso de memoria comparado con listas de Python  
✅ Métodos especializados para álgebra lineal, estadística y cálculos complejos  

### 📂 ¿Qué es un Dataset?

Un **dataset** es un conjunto de datos estructurados que se utilizan para analizar, procesar o entrenar modelos en diferentes disciplinas, como la ciencia de datos, la inteligencia artificial y la estadística. Puedes imaginarlo como una gran hoja de cálculo o una base de datos organizada, donde cada fila representa una observación y cada columna una característica.

Los datasets pueden contener información de muchos tipos, como:                 
📊 Números (precios, cantidades, medidas)  
📊 Texto (nombres, categorías, descripciones)  
📊 Fechas y horas (registro de eventos, historial de cambios)  
📊 Imágenes, sonidos o datos geoespaciales  

### 📊 Dataset de Prueba

En este curso, utilizaremos un **dataset de precios de manzanas** en cinco ciudades rusas durante más de siete años. Este conjunto de datos servirá como base para aplicar los procedimientos de NumPy, permitiéndonos realizar análisis estadísticos, transformaciones y cálculos matemáticos sobre los precios de las manzanas a lo largo del tiempo.

---
## 📥 Introducción al Dataset

El dataset que utilizaremos contiene información sobre el **precio de manzanas** 🍎 en cinco ciudades rusas durante un período de **siete años (2013-2020)**.  
Es un archivo pequeño y sencillo (`apples-ts.csv`), ideal para aprender la funcionalidad de NumPy.  
Además, se creó una **versión modificada** con los nombres de las ciudades traducidos al español.

---

## 💡 ¿Cómo cargar el Dataset en Google Colab?

Tienes dos formas de cargarlo en tu notebook de **Google Colab**:

| 🔄 Método | 📌 Descripción |
|----------|---------------|
| 🔗 Enlace raw desde GitHub | Cargar los datos directamente desde un _gist_ mediante un enlace en formato raw. |
| ☁️ Desde Google Drive | Subir el archivo `manzanas.csv` a Google Drive y acceder a él desde Colab. |

---

## 🧩 Importación de NumPy

```python
import numpy as np
```
Se importa la biblioteca **NumPy** con el alias `np`, una práctica común para simplificar el uso de sus funciones.

---

## 📚 Lectura de Datos con `loadtxt`

Se utiliza la función `np.loadtxt()` para leer los datos del archivo CSV de manera eficiente.

### 🛠️ Parámetros utilizados:
- `delimiter=","` → para indicar que los valores están separados por comas.  
- `usecols=...` → para seleccionar **solo las columnas numéricas**, evitando errores por las etiquetas de texto.

👉 También se emplea `np.arange()` para generar dinámicamente el rango de columnas numéricas a utilizar (excluyendo la primera columna con los nombres de las ciudades).

---

## 📦 Almacenamiento de los Datos

Finalmente, los datos leídos con NumPy se almacenan en una variable llamada `datos`:

```python
datos = np.loadtxt("manzanas.csv", delimiter=",", usecols=np.arange(1, 8))
```

Así tienes un array listo para empezar el análisis.

---

