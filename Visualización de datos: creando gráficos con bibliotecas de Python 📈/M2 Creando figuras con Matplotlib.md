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
# 📊 Creando Subplots en Dos Direcciones con Matplotlib

## 1️⃣ Creación de la matriz de subplots

```python
import matplotlib.pyplot as plt

fig, axs = plt.subplots(2, 2, figsize=(10, 8))
```

* `(2, 2)` → matriz de **2 filas y 2 columnas** = 4 subplots.
* `axs` → ahora es una **matriz bidimensional de ejes**:

  * `axs[0, 0]` → primer subplot (fila 0, col 0).
  * `axs[0, 1]` → segundo subplot (fila 0, col 1).
  * `axs[1, 0]` → tercer subplot (fila 1, col 0).
  * `axs[1, 1]` → cuarto subplot (fila 1, col 1).

---

## 2️⃣ Graficación en subplots individuales

```python
axs[0, 0].plot(años, inmigrantes, marker='o')
axs[0, 0].set_title("Gráfico de Línea")

axs[0, 1].boxplot(inmigrantes)
axs[0, 1].set_title("Boxplot")

axs[1, 0].bar(años, inmigrantes)
axs[1, 0].set_title("Gráfico de Barras")

axs[1, 1].hist(inmigrantes, bins=5)
axs[1, 1].set_title("Histograma")
```

Cada subplot puede tener **tipos de gráficos distintos** (línea, boxplot, barras, histograma, etc.).

---

## 3️⃣ Ajuste de espacios entre subplots

```python
fig.subplots_adjust(hspace=0.4, wspace=0.3)
```

* `hspace` → espacio vertical entre subplots.
* `wspace` → espacio horizontal entre subplots.

---

## 4️⃣ Iteración sobre los subplots

En lugar de configurar cada subplot manualmente:

```python
for ax in axs.flat:  
    ax.set_xlabel("Año")  
    ax.set_ylabel("Inmigrantes")  
    ax.grid(True)  
```

* `axs.flat` → convierte la matriz de ejes en lista 1D.
* Permite aplicar ajustes de forma rápida a todos los subplots.

---

## 5️⃣ Creación de Subgráficos

* **Concepto:** `plt.subplots()` crea una cuadrícula de subgráficos dentro de una sola figura.
* **Ventaja:** permite mostrar y comparar múltiples visualizaciones en un mismo lienzo.

---

## 6️⃣ Ajuste de la escala del eje Y

* **Problema:** al comparar varios gráficos, cada uno puede tener escalas distintas.
* **Solución:** unificamos el rango de valores del eje Y para que la comparación sea justa.

```python
Ymin, Ymax = 0, 2500  

for ax in axs.ravel():  
    ax.set_ylim(Ymin, Ymax)  # misma escala para todos  
```

📌 `axs.ravel()` transforma la matriz 2D de subplots en un array 1D → más fácil de iterar.

---

## 7️⃣ Mejora de la visualización

```python
for ax in axs.ravel():  
    ax.grid(True)  # cuadrícula en cada subplot  

fig.suptitle("Comparación de Inmigración Colombiana (2000-2010)", fontsize=14, fontweight="bold")
```

* `ax.grid()` → añade cuadrícula en cada gráfico.
* `fig.suptitle()` → título general que resume el contenido de toda la figura.

---

## 🔧 Métodos Clave Utilizados

* `plt.subplots()` → crea figura y subplots en cuadrícula.
* `axs.flat` / `axs.ravel()` → recorren todos los subgráficos fácilmente.
* `ax.set_ylim(Ymin, Ymax)` → define límites del eje Y.
* `ax.grid()` → añade cuadrícula.
* `fig.suptitle()` → añade título general a la figura.

---

✅ **Resumen Final:**
Con `plt.subplots()` podemos organizar gráficos en una cuadrícula, unificar escalas con `set_ylim()`, iterar sobre ellos con `axs.ravel()` y mejorar la lectura con cuadrículas y un título general. Esto hace que las comparaciones entre gráficos sean **justas, claras y visualmente consistentes**.

---
# 🎨 Buenas Prácticas para la Visualización de Datos con Subplots 🙌

Cuando trabajamos con **subplots** en Matplotlib, es importante mantener claridad, consistencia y legibilidad en la figura. Aquí algunas recomendaciones:

---

## 1️⃣ Usar títulos claros y concisos

* Cada subplot debe tener un **título breve y descriptivo** para que el lector entienda rápidamente qué está mostrando.
* Si se comparan diferentes conjuntos de datos, puede añadirse un **subtítulo** explicando la relación o diferencia entre ellos.

```python
axs[0, 0].set_title("Tendencia de inmigración")
axs[0, 1].set_title("Distribución por año")
```

---

## 2️⃣ Mantener la misma escala en los ejes

* Para comparaciones justas, es recomendable mantener la **misma escala en los ejes X e Y** en todos los subplots.
* Esto se logra con:

```python
for ax in axs.ravel():
    ax.set_xlim(1980, 2013)   # Escala uniforme en eje X
    ax.set_ylim(0, 2500)      # Escala uniforme en eje Y
```

---

## 3️⃣ Evitar la superposición de gráficos

* Cada subplot debe estar **claramente separado** de los demás.
* Para evitar que los gráficos se amontonen:

  * Ajusta el tamaño de la figura con `figsize`.
  * Usa **espaciado adecuado** con `fig.subplots_adjust()`:

```python
fig.subplots_adjust(hspace=0.4, wspace=0.3)
```

📌 Parámetros importantes:

* `hspace` → controla el espacio **vertical** entre subplots.
* `wspace` → controla el espacio **horizontal** entre subplots.
* El valor es un **decimal** que representa la fracción del tamaño de la figura (ej. `0.5` = 50% de la altura/anchura de la figura).

---

## 4️⃣ Otros consejos adicionales

* **Agregar un título general** con `fig.suptitle()` para contextualizar toda la figura.
* Usar **colores consistentes** entre subplots cuando representen la misma categoría de datos.
* Añadir **cuadrículas (`ax.grid()`)** para facilitar la lectura de valores.
* Evitar saturar los gráficos con demasiada información → cada subplot debe enfocarse en un aspecto particular.

---

✅ **Resumen Final:**
Al usar subplots, cuida que cada gráfico tenga **títulos claros**, **escalas uniformes**, **espaciado suficiente** y un **formato visual consistente**. Esto garantiza que la comparación entre subplots sea **clara, justa y fácil de interpretar**.

---
