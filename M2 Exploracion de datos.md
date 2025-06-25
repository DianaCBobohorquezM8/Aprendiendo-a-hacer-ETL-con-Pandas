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
# 🔢 Escalares, Vectores y Matrices

## ⚫ Escalares

Un **escalar** es un número único y simple, sin dirección, usado comúnmente en operaciones matemáticas básicas como suma o multiplicación.

📌 **Ejemplos**:

* Temperatura: `27 °C`
* Peso: `70 kg`

✅ Representa una **sola cantidad** → es un **dato unidimensional** (`0D` en NumPy).

```python
import numpy as np

escalar = np.array(70)
print(escalar.ndim)  # 0
```

---

## 🟣 Vectores

<img width="310" alt="image" src="https://github.com/user-attachments/assets/74373ac9-f5ac-41dc-9652-3a32a7d04338" />

Un **vector** es una **secuencia de valores**, todos del mismo tipo, que representa múltiples cantidades relacionadas.

📌 **Ejemplos**:

* Pesos de boxeadores: `(70.0, 72.0, 71.2, 70.5)`
* Posición en un plano: `(x, y) = (4, 3)`

🧠 En NumPy, los vectores son arrays **unidimensionales** (`1D`):

```python
vector = np.array([70.0, 72.0, 71.2, 70.5])
print(vector.ndim)  # 1
```

---

## 🟦 Matrices

<img width="138" alt="image" src="https://github.com/user-attachments/assets/e935c8c4-2dfe-4b14-94cb-82fac56895b9" />

Una **matriz** es una estructura bidimensional que representa datos organizados en **filas y columnas**.

📌 **Ejemplo de matriz 2D** (3 filas × 3 columnas):

```python
matriz = np.array([
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
])
print(matriz.shape)  # (3, 3)
print(matriz.ndim)   # 2
```

---

### 🧊 Matrices 3D (y más)

<img width="318" alt="image" src="https://github.com/user-attachments/assets/39b7017d-78cb-442b-8eae-eaf3c840b185" />

Las **matrices tridimensionales** (o más) se utilizan para representar conjuntos de matrices o datos más complejos como:

* 🖼 Procesamiento de imágenes
* 🌀 Animaciones
* 📐 Modelos matemáticos

📌 **Ejemplo de matriz 3D** (2 matrices de 3×3):

```python
matriz_3d = np.array([
    [[1, 2, 3],
     [4, 5, 6],
     [7, 8, 9]],
    
    [[10, 11, 12],
     [13, 14, 15],
     [16, 17, 18]]
])
print(matriz_3d.shape)  # (2, 3, 3)
print(matriz_3d.ndim)   # 3
```

---

## 📏 ¿Qué significa "dimensión"?

| Dimensión | Tipo de estructura        | Varía en...            |
| --------- | ------------------------- | ---------------------- |
| `0D`      | Escalar                   | Ningún eje             |
| `1D`      | Vector                    | Una dimensión (eje)    |
| `2D`      | Matriz                    | Filas y columnas       |
| `3D+`     | Tensor (ej: imágenes RGB) | Más de dos dimensiones |

📌 **Importante**:

* En NumPy: `.ndim` te dice cuántas dimensiones tiene un array.
* `.shape` te muestra la cantidad de elementos en cada dimensión.

---

## ➕ ➗ Operaciones con Matrices

| Operación          | Requisito                                                             |
| ------------------ | --------------------------------------------------------------------- |
| **Suma**           | Mismo número de **filas y columnas**                                  |
| **Multiplicación** | Columnas de la primera matriz deben coincidir con filas de la segunda |

🧠 Por eso, conocer las **dimensiones** de una matriz es crucial antes de realizar operaciones.

---
# 🚫 Tratamiento de NaN en NumPy

Los valores **NaN** (**Not a Number**) indican **datos faltantes o indefinidos**, muy comunes en datasets reales.

---

## ❓ ¿Qué es un NaN?

* Un **NaN** representa un valor **no definido o faltante**.
* Puede aparecer por:

  * ❌ División por cero
  * 📉 Datos no recolectados
  * 🧪 Cálculos inválidos

📌 En NumPy, los NaN son gestionados como valores flotantes especiales.

---

## 🔍 Identificación de NaN

### 🧪 `np.isnan(array)`

Devuelve un **array booleano** donde cada posición es:

* `True` si el valor es `NaN`
* `False` en caso contrario

### ➕ `np.sum(np.isnan(array))`

Cuenta cuántos `NaN` hay sumando los `True` (que valen `1`).

```python
import numpy as np

datos = np.array([1.5, np.nan, 2.5, 3.0])
print(np.isnan(datos))            # [False  True False False]
print(np.sum(np.isnan(datos)))    # 1 (hay un NaN)
```

---

## 🧮 Tratamiento: Interpolación de NaN

La **interpolación lineal** es una técnica común para **rellenar datos faltantes** usando el **promedio de los valores adyacentes**.

```python
datos = np.array([1.5, np.nan, 2.5])

# Interpolación manual
indice_nan = np.where(np.isnan(datos))[0][0]
valor_interp = (datos[indice_nan - 1] + datos[indice_nan + 1]) / 2

datos[indice_nan] = valor_interp
print(datos)  # [1.5, 2.0, 2.5]
```

---

## 📊 Visualización con `Matplotlib`

Visualizar antes y después ayuda a **verificar que el NaN fue tratado correctamente**.

```python
import matplotlib.pyplot as plt

fechas = ["Ene", "Feb", "Mar"]
datos = [1.5, 2.0, 2.5]

plt.plot(fechas, datos)
plt.title("Interpolación de datos faltantes")
plt.xlabel("Mes")
plt.ylabel("Precio")
plt.show()
```

---

## 🧼 Cálculos con datos limpios

Una vez tratados los `NaN`, puedes realizar operaciones como:

```python
precio_promedio = np.mean(datos)
print(precio_promedio)  # Promedio sin errores por NaN
```

---

## 🧠 Resumen rápido

| Acción                       | Función / Método                      |
| ---------------------------- | ------------------------------------- |
| Detectar `NaN`               | `np.isnan(array)`                     |
| Contar `NaN`                 | `np.sum(np.isnan(array))`             |
| Reemplazar con interpolación | Cálculo manual con valores adyacentes |
| Visualizar datos             | `plt.plot(x, y)`                      |
| Calcular promedio limpio     | `np.mean(array)`                      |

---
## 🧮 Contar valores `NaN` en un array

Cuando queremos **contar cuántos valores faltantes (`NaN`) hay en un array**, usamos una combinación de funciones:

### ✅ Opción correcta y más eficiente:

```python
np.sum(np.isnan(jugo_de_limon))
```

### 🔁 Alternativa posible:

```python
sum(np.isnan(jugo_de_limon))
```

---

### 🧠 ¿Qué hacen estas funciones?

1. **`np.isnan(jugo_de_limon)`**
   → Devuelve un array booleano con `True` donde hay `NaN` y `False` donde no:

   ```python
   # Ejemplo
   array = np.array([1.0, np.nan, 2.0])
   np.isnan(array)  # Resultado: [False, True, False]
   ```

2. **`np.sum(...)`**
   → Suma los `True` (que valen `1`) y los `False` (que valen `0`), devolviendo la **cantidad total de NaN**.

---

### ✅ Recomendación:

| Método                  | Recomendado | Por qué                                                |
| ----------------------- | ----------- | ------------------------------------------------------ |
| `np.sum(np.isnan(...))` | ✅ Sí        | Funciona con arrays multidimensionales y es más rápido |
| `sum(np.isnan(...))`    | ⚠️ A veces  | Funciona solo con arrays unidimensionales              |

    ✅Unidimensional: Una sola línea de elementos.
    ⚠️ Multidimensional: Una estructura con filas, columnas y posiblemente más dimensiones.
---

### 📌 Ejemplo completo:

```python
import numpy as np

jugo_de_limon = np.array([1.0, np.nan, 2.5, np.nan])
total_nan = np.sum(np.isnan(jugo_de_limon))
print("Total de NaN:", total_nan)  # Output: 2
```
---
