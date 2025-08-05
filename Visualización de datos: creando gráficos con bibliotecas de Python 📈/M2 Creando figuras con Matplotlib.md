# 📈 Módulo 2 : Creando figuras con Matplotlib 📈
---
# 🎨 Creando una Figura y Ejes en Matplotlib

---

## 1️⃣ Creación de la figura y los ejes

```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots(figsize=(8, 4))
```

* **Concepto:**

  * `fig` = el **lienzo completo** 🖼️ (toda la hoja donde dibujarás).
  * `ax` = los **ejes** 📐 (la parte donde realmente se trazan los datos).
* **Analogía:** Es como tener una hoja de papel (figura) y en ella dibujar un recuadro (ejes) donde harás tu gráfico.

---

## 2️⃣ Graficar datos en los ejes

```python
ax.plot(años, inmigrantes, marker='o', linestyle='-', color='b')
```

* **Concepto:** Dibuja un gráfico de líneas dentro del objeto `ax`.
* **Parámetros comunes:**

  * `marker='o'` → marca puntos en cada dato.
  * `linestyle='-'` → línea continua.
  * `color='b'` → azul.
* **Analogía:** Usar el pincel dentro de un recuadro en tu hoja para trazar la línea.

---

## 3️⃣ Ajustar dinámicamente los ticks del eje X

```python
import matplotlib.ticker as ticker

locator = ticker.MultipleLocator(base=1.0)   # ticks cada 1 unidad
ax.xaxis.set_major_locator(locator)
```

* **Concepto:** Controla qué tan espaciadas aparecen las marcas en el eje X.
* **Analogía:** Es como decidir cada cuánto pones una marca en una regla 📏 (cada 1 cm, cada 5 cm, etc.).

---

## 4️⃣ Añadir título y rótulos

```python
ax.set_title("Inmigración de colombianos hacia Canadá\n(1980-2013)", 
             fontdict={'fontsize': 12, 'fontweight': 'bold'})
ax.set_xlabel("Año", fontdict={'fontsize': 10})
ax.set_ylabel("Número de Inmigrantes", fontdict={'fontsize': 10})
```

* **Concepto:**

  * `set_title()` → título general del gráfico.
  * `set_xlabel()` → etiqueta eje X.
  * `set_ylabel()` → etiqueta eje Y.
* **Analogía:** Es como ponerle título y leyendas a un mapa 🗺️ para que cualquiera entienda qué representan los caminos y símbolos.

---

## 5️⃣ Mostrar el gráfico

```python
plt.show()
```

📌 Muestra el gráfico completo.

---

## 6️⃣ Ejemplo completo

```python
import matplotlib.pyplot as plt
import matplotlib.ticker as ticker

años = list(range(2000, 2010))
inmigrantes = [500, 700, 800, 1200, 1500, 1600, 1400, 1800, 2000, 2200]

# Crear figura y ejes
fig, ax = plt.subplots(figsize=(10, 5))

# Graficar
ax.plot(años, inmigrantes, marker='o', linestyle='-', color='b')

# Ajustar ticks dinámicos
locator = ticker.MultipleLocator(base=1.0)
ax.xaxis.set_major_locator(locator)

# Título y etiquetas
ax.set_title("Inmigración de colombianos hacia Canadá\n(2000-2009)", 
             fontdict={'fontsize': 12, 'fontweight': 'bold'})
ax.set_xlabel("Año", fontdict={'fontsize': 10})
ax.set_ylabel("Número de Inmigrantes", fontdict={'fontsize': 10})

# Mostrar
plt.show()
```

---

✅ **Resumen:**

* `fig, ax = plt.subplots()` → crea lienzo y ejes.
* `ax.plot()` → dibuja la línea.
* `ax.set_title(), ax.set_xlabel(), ax.set_ylabel()` → personaliza.
* `ticker.MultipleLocator()` → controla los ticks.
* `plt.show()` → muestra el gráfico final.

---
# 📊 Creando Subplots en una Dirección con Matplotlib

---

## 1️⃣ ¿Qué son los subplots?

Son **gráficos múltiples en una misma figura**.

* Sirven para comparar datos de forma clara y organizada.
* Se pueden organizar en **filas** y **columnas**.

👉 Ejemplo: una fila con 2 gráficos → un gráfico de línea + un boxplot.

---

## 2️⃣ Creación de la figura y subgráficos

```python
import matplotlib.pyplot as plt

fig, axs = plt.subplots(1, 2, figsize=(12, 5))  
```

* `1, 2` → significa **1 fila y 2 columnas** (dos gráficos en horizontal).
* `axs` es un **array de ejes**:

  * `axs[0]` → primer gráfico.
  * `axs[1]` → segundo gráfico.

---

## 3️⃣ Gráfico de líneas en el primer subplot

```python
axs[0].plot(años, inmigrantes, marker='o', color='b')
axs[0].set_title("Inmigración de colombianos hacia Canadá")
axs[0].set_xlabel("Año")
axs[0].set_ylabel("Número de inmigrantes")
axs[0].grid()
```

* Línea de inmigrantes a lo largo del tiempo.
* `grid()` ayuda a leer mejor los valores.

---

## 4️⃣ Boxplot en el segundo subplot

```python
axs[1].boxplot(inmigrantes)
axs[1].set_title("Distribución de inmigración")
axs[1].set_xlabel("Colombia")
axs[1].set_ylabel("Número de inmigrantes")
axs[1].grid()
```

* 📦 El **boxplot** muestra:

  * Línea dentro → **mediana (50%)**.
  * Caja inferior y superior → **Q1 (25%) y Q3 (75%)**.
  * Bigotes → **mínimo y máximo**.
  * Outliers → puntos extremos.

---

## 5️⃣ Mostrar todo

```python
plt.show()
```

---

## 6️⃣ Estadísticas descriptivas con Pandas

```python
import pandas as pd

# Ejemplo usando el DataFrame datos_col
print(datos_col.describe())
```

📌 Devuelve:

* **count** → número de registros.
* **mean** → promedio.
* **std** → desviación estándar.
* **min, 25%, 50%, 75%, max** → resumen de la distribución.

---

## 🔎 Ejemplo completo

```python
import matplotlib.pyplot as plt
import pandas as pd

años = list(range(2000, 2010))
inmigrantes = [500, 700, 800, 1200, 1500, 1600, 1400, 1800, 2000, 2200]

# Crear figura con 2 subplots en una fila
fig, axs = plt.subplots(1, 2, figsize=(12, 5))

# Gráfico de línea
axs[0].plot(años, inmigrantes, marker='o', color='b')
axs[0].set_title("Inmigración de colombianos hacia Canadá")
axs[0].set_xlabel("Año")
axs[0].set_ylabel("Número de inmigrantes")
axs[0].grid()

# Boxplot
axs[1].boxplot(inmigrantes)
axs[1].set_title("Distribución de inmigración")
axs[1].set_xlabel("Colombia")
axs[1].set_ylabel("Número de inmigrantes")
axs[1].grid()

# Mostrar
plt.show()

# Estadísticas descriptivas
datos_col = pd.DataFrame({"año": años, "inmigrantes": inmigrantes})
print(datos_col.describe())
```

---

✅ **Resumen:**

* `plt.subplots(filas, columnas)` → define distribución de subplots.
* `axs[i].plot()` → gráfico de líneas en un subplot.
* `axs[i].boxplot()` → boxplot en otro subplot.
* `datos.describe()` → estadísticas numéricas que complementan la visualización.

---
