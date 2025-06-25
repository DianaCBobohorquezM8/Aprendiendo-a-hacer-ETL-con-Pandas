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

### 📂 ¿Qué es un Dataset?

Un **dataset** es un conjunto de datos estructurados que se utilizan para analizar, procesar o entrenar modelos en diferentes disciplinas, como la ciencia de datos, la inteligencia artificial y la estadística. Puedes imaginarlo como una gran hoja de cálculo o una base de datos organizada, donde cada fila representa una observación y cada columna una característica.

Los datasets pueden contener información de muchos tipos, como:                 
📊 Números (precios, cantidades, medidas)  
📊 Texto (nombres, categorías, descripciones)  
📊 Fechas y horas (registro de eventos, historial de cambios)  
📊 Imágenes, sonidos o datos geoespaciales  

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
# 🍏Visualización de Datos con NumPy y Matplotlib

## 🧩 Slice Notation (Notación de Segmento)

La **notación de segmento** permite seleccionar partes específicas de un array:

```python
array[inicio:fin:paso]
```

## ✂️ Slice Notation en Python y NumPy

### 🧱 Estructura Básica

| Parámetro | Significado                                         | Valor por defecto |
| --------- | --------------------------------------------------- | ----------------- |
| `inicio`  | Índice desde donde empieza la selección (incluido)  | `0`               |
| `fin`     | Índice donde termina la selección (**no incluido**) | Hasta el final    |
| `paso`    | Intervalo entre los elementos seleccionados         | `1`               |


📌 **Ejemplo**:

```python
import numpy as np

a = np.array([10, 20, 30, 40, 50, 60])
print(a[1:5:2])  # [20 40]
```
---

### 🔍 Ejemplo simple con una lista

```python
array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

| Expresión    | Resultado         | Descripción                                  |
| ------------ | ----------------- | -------------------------------------------- |
| `array[2:5]` | `[2, 3, 4]`       | Desde el índice 2 hasta el 4 (5 no incluido) |
| `array[:5]`  | `[0, 1, 2, 3, 4]` | Desde el inicio hasta el índice 4            |
| `array[5:]`  | `[5, 6, 7, 8, 9]` | Desde el índice 5 hasta el final             |
| `array[::2]` | `[0, 2, 4, 6, 8]` | Cada 2 elementos (paso = 2)                  |

---

### 🧮 Aplicación en matrices (arrays 2D con NumPy)

Cuando trabajas con matrices, la notación se aplica **por dimensión**:

```python
import numpy as np

matriz = np.array([
    [10, 20, 30],
    [40, 50, 60],
    [70, 80, 90]
])
```

| Expresión          | Resultado                     | Descripción                                    |
| ------------------ | ----------------------------- | ---------------------------------------------- |
| `matriz[:, 1:3]`   | `[[20 30], [50 60], [80 90]]` | Todas las filas (`:`) y columnas 1 y 2 (`1:3`) |
| `matriz[0:2, :]`   | `[[10 20 30], [40 50 60]]`    | Filas 0 y 1, todas las columnas                |
| `matriz[::2, ::2]` | `[[10 30], [70 90]]`          | Saltando de 2 en 2 en filas y columnas         |

---

### 💡 Tip útil

La notación de segmento es **muy poderosa** cuando se combina con otras operaciones como transposición o filtrado. Dominarla te permitirá hacer manipulaciones complejas de arrays con muy poco código.


---

## 🔁 Transposición de Datos

Permite **intercambiar filas por columnas**.

| Método           | Descripción                        |
| ---------------- | ---------------------------------- |
| `.T`             | Transposición directa              |
| `np.transpose()` | Función de transposición explícita |

📌 **Ejemplo**:

```python
array = np.array([[1, 2], [3, 4]])
print(array.T)
# [[1 3]
#  [2 4]]
```

🧠 **Relación**:
La transposición cambia la estructura de los datos, **facilitando el acceso por segmentos** (ej. convertir fechas en columnas).

---
## 📈 Gráficas con Matplotlib

Las **gráficas** son representaciones visuales de datos que permiten identificar patrones, tendencias y variaciones de forma intuitiva.

🎯 **Objetivo**:
Visualizar los datos manipulados con **NumPy** mediante la biblioteca **Matplotlib**, facilitando su interpretación.

---

### 📊 Matplotlib

`Matplotlib` es una biblioteca de Python ampliamente utilizada para **crear visualizaciones** de datos.

| Función        | Descripción                    |
| -------------- | ------------------------------ |
| `plt.plot()`   | Crea un gráfico de líneas      |
| `plt.title()`  | Agrega un título a la gráfica  |
| `plt.xlabel()` | Etiqueta para el eje X         |
| `plt.ylabel()` | Etiqueta para el eje Y         |
| `plt.show()`   | Muestra la gráfica en pantalla |

📌 **Ejemplo práctico**:

```python
import matplotlib.pyplot as plt

fechas = ["Ene", "Feb", "Mar"]
precios = [100, 120, 110]

plt.plot(fechas, precios)
plt.title("Precios de Manzanas")
plt.xlabel("Mes")
plt.ylabel("Precio")
plt.show()
```
---

### 📉 Ejes X e Y

Los **ejes** son fundamentales para dar contexto y sentido a la gráfica:

| Eje | Representa          | Ejemplo                 |
| --- | ------------------- | ----------------------- |
| `X` | Tiempo o categorías | `["Ene", "Feb", "Mar"]` |
| `Y` | Valores medidos     | `[100, 120, 110]`       |

🧠 **Importancia**:
Asignar correctamente los datos a cada eje es esencial para una **interpretación precisa** del gráfico.

---
## 🍏 Resumen General

| Concepto       | Herramienta              | Relación clave                                  |
| -------------- | ------------------------ | ----------------------------------------------- |
| Slice Notation | `array[inicio:fin:paso]` | Extraer subconjuntos de datos                   |
| Transposición  | `.T` o `transpose()`     | Cambiar orientación de los datos                |
| Visualización  | `Matplotlib`             | Crear gráficos de líneas con `plt.plot()`       |
| Ejes X e Y     | `xlabel()` y `ylabel()`  | Claridad en qué se mide y contra qué se compara |

---
# 📘✨ Comparación de Arrays y Visualización con Matplotlib🔍

## 🟰 Comparación entre Arrays con NumPy

Comparar arrays es esencial para verificar si contienen la misma información o si son **suficientemente similares** para fines prácticos.

### 🧪 `numpy.array_equal(a, b)`

Compara dos arrays y devuelve `True` si:

* Tienen la **misma forma**
* Tienen los **mismos elementos** en las **mismas posiciones**

📌 **Ejemplo**:

```python
import numpy as np

array1 = np.array([1, 2, 3])
array2 = np.array([1, 2, 3])
array3 = np.array([4, 5, 6])

print(np.array_equal(array1, array2))  # True (idénticos)
print(np.array_equal(array1, array3))  # False (diferentes)
```

🔒 **Nota**: Esta comparación es **estricta**, útil cuando se necesita igualdad exacta.

---

### 🤏`numpy.allclose(a, b, rtol=1e-05, atol=1e-08)`

Permite comparar arrays con valores **aproximadamente iguales**, tolerando diferencias pequeñas (por ejemplo, por redondeo).

#### 📐 Parámetros:

| Parámetro | Significado                                |
| --------- | ------------------------------------------ |
| `a`, `b`  | Arrays a comparar                          |
| `rtol`    | Tolerancia relativa (por defecto: `1e-05`) |
| `atol`    | Tolerancia absoluta (por defecto: `1e-08`) |

📘 **Fórmula usada**:

```python
abs(a - b) <= (atol + rtol * abs(b))
```

📌 **Ejemplo**:

```python
array1 = np.array([1.0, 2.0, 3.0])
array2 = np.array([1.0001, 2.0002, 3.0003])
array3 = np.array([1.1, 2.2, 3.3])

print(np.allclose(array1, array2))           # True (diferencia mínima)
print(np.allclose(array1, array3))           # False (diferencia grande)
print(np.allclose(array1, array3, atol=0.2))  # True (si aumentamos la tolerancia)
```

✅ **Resumen**:

| Función            | Uso principal                           | Tolerancia |
| ------------------ | --------------------------------------- | ---------- |
| `np.array_equal()` | Verifica igualdad exacta                | ❌ No       |
| `np.allclose()`    | Compara arrays con pequeñas diferencias | ✅ Sí       |

---

## 📊 Visualización con Matplotlib

Una parte esencial del análisis de datos es representar los resultados visualmente. `Matplotlib` permite crear gráficos para **comparar visualmente arrays**, por ejemplo, precios de manzanas por año.

---

### 📅Crear el eje X con `numpy.arange()`

```python
import numpy as np

meses = np.arange(1, 13, 1)  # De 1 a 12 (meses del año)
```

| Parámetro | Descripción              | Ejemplo |
| --------- | ------------------------ | ------- |
| `start`   | Valor inicial (incluido) | `1`     |
| `stop`    | Valor final (excluido)   | `13`    |
| `step`    | Incremento entre valores | `1`     |

---

### 📈Dibujar líneas con `plt.plot(x, y)`

```python
import matplotlib.pyplot as plt

precios_2013 = [100, 110, 105, 120, 115, 130, 125, 140, 135, 150, 145, 160]
precios_2014 = [102, 112, 108, 118, 117, 132, 128, 142, 138, 152, 147, 162]

plt.plot(meses, precios_2013)
plt.plot(meses, precios_2014)
```

🔹 **`x` = meses**, **`y` = precios por mes**

---

### 🏷️Agregar leyenda con `plt.legend()`

```python
plt.legend(["2013", "2014"])
```

Esto muestra una **leyenda** para identificar cada línea del gráfico.

---

### 🎨Mostrar la gráfica completa

```python
plt.title("Precios de Manzanas por Año")
plt.xlabel("Mes")
plt.ylabel("Precio")
plt.show()
```

---

## 📌 Resumen del flujo completo

1. **`np.arange()`** genera los valores del eje X (meses).
2. **`plt.plot()`** dibuja líneas de precios por año.
3. **`plt.legend()`** agrega etiquetas a cada línea.
4. **`plt.show()`** muestra la gráfica final.
---


