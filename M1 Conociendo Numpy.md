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

# 🧠 Ventajas de los Arrays en Python con NumPy

## 🔢 ¿Qué son las listas y arrays?

* **Listas**: estructuras básicas de Python que pueden contener distintos tipos de datos (`int`, `str`, otras listas...).
* **NumPy Arrays**: estructuras optimizadas y eficientes para cálculos numéricos, provistas por la biblioteca `NumPy`.

---

## 🔁 Conversión de lista a array

```python
import numpy as np

# Crear una lista
lista = [1, 2, 3, 4, 5]

# Convertirla a array
array = np.array(lista)

print("Lista: ", lista)
print("Array: ", array)
```

📤 **Salida**:

```
Lista: [1, 2, 3, 4, 5]
Array: [1 2 3 4 5]
```

---

## ✅ Ventajas de los Arrays NumPy

| Ventaja                       | Descripción                                                                |
| ----------------------------- | -------------------------------------------------------------------------- |
| ⚡ Eficiencia de procesamiento | Más rápidos en operaciones matemáticas. Libera memoria de forma eficiente. |
| ✍️ Código más limpio          | Operaciones matemáticas más concisas y legibles.                           |
| 🔗 Integración                | Se integra fácilmente con librerías como **Pandas**, **Matplotlib**, etc.  |

---

## 🧪 Comparación de Rendimiento: Lista vs Array

```python
import numpy as np
import time

# Lista con 1 millón de elementos
lista = list(range(1000000))
array = np.array(lista)

# Tiempo con lista
start = time.time()
lista_cuadrado = [i**2 for i in lista]
tiempo_lista = time.time() - start

# Tiempo con array
start = time.time()
array_cuadrado = array**2
tiempo_array = time.time() - start

print("⏱️ Tiempo con lista:", tiempo_lista)
print("⏱️ Tiempo con array:", tiempo_array)
```

📤 **Salida**:

```
⏱️ Tiempo con lista: 0.2746 s
⏱️ Tiempo con array: 0.0041 s
```

✅ **Conclusión**:
El uso de `NumPy` permite una **mejora significativa en rendimiento**, especialmente con grandes volúmenes de datos.

---
# 🧮 Dimensiones y Forma de los Arrays 

## 📥 Creación del Array

Se creó un array a partir de un dataset y se almacenó en una variable llamada `Datos` para su posterior análisis:

```python
import numpy as np

# Supongamos que este es el array de ejemplo
Datos = np.array([
    [100, 200, 150],
    [110, 210, 160],
    [120, 220, 170],
    [130, 230, 180],
    [140, 240, 190],
    [150, 250, 200],
])
```

---

## 🔍 Información clave del Array

### 📏 Dimensiones del Array (`.ndim`)

| Atributo      | Descripción                                                                                                                |
| ------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `.ndim`       | Devuelve el número de **dimensiones** (ejes) del array.                                                                    |
| 🛠 Aplicación | `Datos.ndim` devuelve `2`, lo que indica que el array tiene **2 dimensiones**: una para los meses y otra para los precios. |

```python
print("Dimensiones:", Datos.ndim)  # Salida: 2
```

---

### 📐 Forma del Array (`.shape`)

| Atributo      | Descripción                                                                 |
| ------------- | --------------------------------------------------------------------------- |
| `.shape`      | Devuelve una **tupla (filas, columnas)** que representa la forma del array. |
| 🛠 Aplicación | `Datos.shape` devolvió `(6, 87)`, indicando que hay 6 filas y 87 columnas.  |

```python
print("Forma:", Datos.shape)  # Ejemplo de salida: (6, 87)
```

---

### 🔄 Transposición del Array (`.T` o `transpose()`)

| Atributo              | Descripción                                                                                                                               |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `.T` o `.transpose()` | Transpone el array: **intercambia filas por columnas**.                                                                                   |
| 🛠 Aplicación         | Facilita la visualización cuando hay muchos datos por fila. Por ejemplo, convierte los **meses en columnas** y las **ciudades en filas**. |

```python
datos_transpuestos = Datos.T
print(datos_transpuestos.shape)  # Ejemplo de salida: (87, 6)
```

---

## 💾 Almacenamiento de datos transpuestos

Se asignó el resultado de la transposición a una nueva variable llamada `datos_transpuestos` para facilitar análisis posteriores.

```python
# Guardar transposición para uso futuro
datos_transpuestos = Datos.T
```

---

## 🧠 Resumen General

| Método/Atributo       | Qué hace 📌                                 | Ejemplo de uso                 |
| --------------------- | ------------------------------------------- | ------------------------------ |
| `.ndim`               | Devuelve el número de dimensiones del array | `Datos.ndim → 2`               |
| `.shape`              | Devuelve tupla con filas y columnas         | `Datos.shape → (6, 87)`        |
| `.T` o `.transpose()` | Transpone el array (filas ↔ columnas)       | `Datos.T.shape → (87, 6)`      |
| Variable nueva        | Guarda el resultado para análisis futuros   | `datos_transpuestos = Datos.T` |

---


