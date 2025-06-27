
# 📉 Línea Recta y Comparación de Arrays en NumPy

## 🧮 Función de Línea Recta

La **ecuación de una recta** es:

```text
Y = A * X + B
```

| Símbolo | Significado                        |
| ------- | ---------------------------------- |
| `A`     | Pendiente (cambio por unidad de X) |
| `X`     | Variable independiente (fechas)    |
| `B`     | Intersección en el eje Y           |
| `Y`     | Valor estimado (precio)            |

```python
X = fechas
Y = 1.5 * X + 78  # Línea recta estimada
```

---

## 🔍 Visualización con `matplotlib`

Superponemos los datos reales y la estimación para comparar visualmente:

```python
import matplotlib.pyplot as plt

plt.plot(fechas, Moscu, label="Precios Reales")
plt.plot(X, Y, label="Línea Estimada", linestyle="--")
plt.title("Ajuste de Línea Recta")
plt.xlabel("Meses")
plt.ylabel("Precio")
plt.legend()
plt.show()
```

---

## 🔄 Comparación entre Arrays

### 🔹 Resta de Arrays

```python
diferencia = Moscu - Y
```

Nos da la diferencia **elemento por elemento** entre los precios reales y los estimados.

### 🔹 Ajuste Manual

Modificamos la pendiente para mejorar el ajuste:

```python
Y = 0.5 * X + 78
```

➡️ Así se reduce la diferencia total.

---

## 📏 Medición de la Diferencia Total

### 🧠 Método Manual (Raíz de la suma de cuadrados)

```python
np.sqrt(np.sum(np.power(Moscu - Y, 2)))
```

| Paso               | Explicación                                       |
| ------------------ | ------------------------------------------------- |
| `Moscu - Y`        | Diferencias individuales                          |
| `np.power(..., 2)` | Cuadrado de cada diferencia                       |
| `np.sum(...)`      | Suma total de los cuadrados                       |
| `np.sqrt(...)`     | Raíz cuadrada: diferencia total (tipo Euclidiana) |

---

### 🧪 Método Elegante: `np.linalg.norm`

```python
np.linalg.norm(Moscu - Y)
```

Hace exactamente lo mismo que el cálculo manual pero de forma directa y eficiente.

---

## 🧠 Conceptos Clave

| Concepto                  | Definición                                                      |
| ------------------------- | --------------------------------------------------------------- |
| **Función lineal**        | Modelo matemático simple para representar una tendencia         |
| **Estimación de datos**   | Ajuste de una recta a datos observados                          |
| **Resta de arrays**       | Diferencia entre los valores estimados y los reales             |
| **Norma (`linalg.norm`)** | Medida de la magnitud total de un vector (errores en este caso) |

---

## ✅ Comparación Visual

| Método                 | ¿Qué hace?                         | Ventaja                    |
| ---------------------- | ---------------------------------- | -------------------------- |
| `Moscu - Y`            | Diferencia punto a punto           | Identifica errores locales |
| `np.sqrt(np.sum(...))` | Diferencia total (cuadrática)      | Penaliza errores grandes   |
| `np.linalg.norm(...)`  | Mismo resultado, código más limpio | Eficiencia y claridad      |

---
# 📊 Regresión Lineal

La **regresión lineal** es un método estadístico que nos permite modelar la relación entre dos variables:

* `X`: Variable independiente (fechas)
* `Y`: Variable dependiente (precios)

Usamos NumPy para realizar los cálculos fundamentales, como la **pendiente** y la **intersección** de la recta.

---

## 📐 Componentes Clave

| Concepto              | Descripción                                            |
| --------------------- | ------------------------------------------------------ |
| 🧮 Pendiente (`α`)    | Mide cuánto cambia `Y` por cada unidad que cambia `X`. |
| 🎯 Intersección (`β`) | Valor de `Y` cuando `X = 0`.                           |
| 📊 N (observaciones)  | Número total de pares `(X, Y)` utilizados.             |
| ➕ Sumatoria           | Suma de todos los elementos de un conjunto de datos.   |
| 📉 Promedio           | Media aritmética: suma total ÷ número de elementos.    |

---

## 📎 Fórmulas de la Regresión

### 🧮 Pendiente (`α`)

$$
\alpha = \frac{N \cdot \sum(X \cdot Y) - \sum X \cdot \sum Y}{N \cdot \sum(X^2) - (\sum X)^2}
$$

### 📍 Intersección (`β`)

$$
\beta = \overline{Y} - \alpha \cdot \overline{X}
$$

---

## 🧪 Cálculo con NumPy

```python
import numpy as np

# Datos ficticios
X = np.array([1, 2, 3, 4, 5])
Y = np.array([2, 4, 5, 4, 5])
N = len(X)

# Pendiente (α)
alfa = (N * np.sum(X * Y) - np.sum(X) * np.sum(Y)) / (N * np.sum(X**2) - np.sum(X)**2)

# Intersección (β)
beta = np.mean(Y) - alfa * np.mean(X)

print(f"Pendiente: {alfa}")
print(f"Intersección: {beta}")
```

---

## 📚 Funciones NumPy utilizadas

### 🔢 `np.sum(array, axis=None)`

| Parámetro | Descripción                            |
| --------- | -------------------------------------- |
| `array`   | Array del que se desea obtener la suma |
| `axis=0`  | Suma por columnas                      |
| `axis=1`  | Suma por filas                         |

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(np.sum(arr))          # 21
print(np.sum(arr, axis=0))  # [5 7 9]
print(np.sum(arr, axis=1))  # [6 15]
```

---

### 📏 `np.mean(array, axis=None)`

| Parámetro | Descripción                                |
| --------- | ------------------------------------------ |
| `array`   | Array del que se desea obtener el promedio |
| `axis=0`  | Promedio por columnas                      |
| `axis=1`  | Promedio por filas                         |

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(np.mean(arr))          # 3.5
print(np.mean(arr, axis=0))  # [2.5 3.5 4.5]
print(np.mean(arr, axis=1))  # [2. 5.]
```
---
## ✍️ Anotación en LaTeX

Usamos **LaTeX** para expresar fórmulas matemáticas con claridad, especialmente útil en entornos como Jupyter Notebook o documentación científica.

### 💡 ¿Qué es LaTeX?

**LaTeX** (se pronuncia *la-tej* o *lei-tek*) es un lenguaje de marcado diseñado para escribir documentos científicos y fórmulas matemáticas con una presentación **clara, precisa y profesional**.

Aunque fue creado para escribir documentos completos, su sistema de fórmulas matemáticas se ha convertido en **el estándar en ciencia, matemática, ingeniería y programación**, y es muy usado dentro de herramientas como:

* **Jupyter Notebook**
* **Markdown con soporte matemático**
* **Kaggle Notebooks**
* **Google Colab**
* **Latexify en Python**

---

### ✅ ¿Por qué usar LaTeX?

🔹 Permite escribir **fórmulas complejas** de forma estructurada.
🔹 Mejora la **legibilidad y presentación** de los cálculos matemáticos.
🔹 Es compatible con muchos entornos de análisis de datos.

---

### 📌 Sintaxis Básica

| Tipo de elemento     | Código LaTeX                                              | Ejemplo renderizado                                       |
| -------------------- | --------------------------------------------------------- | --------------------------------------------------------- |
| Suma                 | `\sum x_i`                                                | $\sum x_i$                                                |
| Promedio             | `\frac{\sum x}{n}`                                        | $\frac{\sum x}{n}$                                        |
| Potencia             | `x^2`                                                     | $x^2$                                                     |
| Subíndice            | `x_1`                                                     | $x_1$                                                     |
| Raíz cuadrada        | `\sqrt{x}`                                                | $\sqrt{x}$                                                |
| Ecuación de recta    | `y = \alpha x + \beta`                                    | $y = \alpha x + \beta$                                    |
| Fórmula de pendiente | `\frac{n\sum xy - \sum x \sum y}{n\sum x^2 - (\sum x)^2}` | $\frac{n\sum xy - \sum x \sum y}{n\sum x^2 - (\sum x)^2}$ |

---

### 🧠 ¿Dónde lo uso?

📌 **Jupyter Notebook (Python + Markdown)**
Para escribir ecuaciones:

```markdown
Ecuación de la recta:

$y = \alpha x + \beta$
```

📌 **Markdown normal** (en plataformas compatibles):
Usa `$...$` para inline y `$$...$$` para bloque:

```markdown
Inline: $y = mx + b$

Bloque:
$$
\alpha = \frac{n\sum xy - \sum x \sum y}{n\sum x^2 - (\sum x)^2}
$$
```

📌 **Google Colab**
Puedes usar LaTeX directamente en celdas de texto:

```markdown
$$ y = \alpha x + \beta $$
```

---

### ✨ Tip: Cómo leer una fórmula en LaTeX

Tomemos esta fórmula de la pendiente:

```latex
\alpha = \frac{n\sum xy - \sum x \sum y}{n\sum x^2 - (\sum x)^2}
```

📖 **Traducción paso a paso:**

* `\alpha` → letra griega alfa, representa la pendiente.
* `\frac{a}{b}` → fracción: a arriba, b abajo.
* `\sum` → símbolo de suma.
* `xy` → producto de X e Y.
* `x^2` → X al cuadrado.
* `(\sum x)^2` → la suma de X, todo al cuadrado.

---

## 🔚 Conclusión

✨ Usar LaTeX te permite documentar tus análisis de forma clara y elegante.
💼 Ideal para notebooks, informes y presentaciones técnicas.

---
## 📐 Regresión Lineal y la Ecuación de la Recta

### 📊 ¿Qué es la regresión lineal?

La **regresión lineal simple** es un método estadístico que nos permite modelar la relación entre una **variable independiente** (como el mes del año) y una **variable dependiente** (como el precio de las manzanas). Utilizamos este modelo para **predecir valores** o **analizar tendencias**.

---

## 📏 Ecuación de la línea recta:

$$
y = ax + b
$$

| Símbolo | Significado                                                     |
| ------- | --------------------------------------------------------------- |
| $y$     | Valor a predecir (por ejemplo, el precio de la manzana)         |
| $x$     | Valor conocido (por ejemplo, el número del mes)                 |
| $a$     | Pendiente (indica cuánto varía el precio por cada mes que pasa) |
| $b$     | Intersección (valor del precio estimado cuando $x = 0$)         |

---

### 🔢 Ejemplo en NumPy

```python
import numpy as np
import matplotlib.pyplot as plt

# Suponiendo que los meses van del 1 al 12
x = np.arange(1, 13)

# Ecuación: y = a * x + b
a = 1.2  # Pendiente
b = 78   # Intersección
y = a * x + b

plt.plot(x, y, label="Modelo Lineal")
plt.xlabel("Mes")
plt.ylabel("Precio (COP)")
plt.title("Predicción de precios de manzana")
plt.legend()
plt.show()
```

---

## 🔮 Predicción de Precios

Sustituimos valores de $x$ en la ecuación para **predecir precios futuros**.
Por ejemplo, para el mes 10:

```python
mes = 10
precio_estimado = a * mes + b
print(precio_estimado)  # Resultado: 90.0
```

Esto nos permite estimar cuánto costaría la manzana en ese mes según la tendencia.

---

## ⚠️ Limitaciones del Modelo Lineal

Aunque útil, una **línea recta no siempre describe bien** datos reales, especialmente si:

* Hay mucha variabilidad mes a mes.
* Los precios suben y bajan sin un patrón lineal.

Esto nos lleva al concepto de:

### 🧠 Overfitting (Sobreajuste)

Cuando usamos **modelos demasiado complejos** (como polinomios de alto grado), podemos "forzar" que se ajusten exactamente a los datos existentes.
Esto parece bueno, pero en realidad **pierde capacidad de generalizar** a nuevos datos.

🔎 Ejemplo visual:

* ✅ Una línea simple puede capturar la **tendencia general**.
* ❌ Un polinomio de grado 10 puede capturar **cada punto**, pero fallar en futuras predicciones.

---

## 🧪 Alternativas con NumPy

En lugar de ajustar manualmente $a$ y $b$, podemos usar:

* `np.random` para **probar valores aleatorios de pendiente e intersección**
* Técnicas como **mínimos cuadrados** o usar `np.polyfit()` para obtener el mejor ajuste automático.

### Ejemplo con `np.polyfit`:

```python
# Suponiendo que x = meses, y = precios reales
a, b = np.polyfit(x, y_real, 1)  # Ajuste automático de la mejor recta
y_pred = a * x + b
```

---

## ✅ Conclusión

* La ecuación de la recta es una **herramienta clave** en análisis predictivo.
* Nos ayuda a **visualizar y estimar** comportamientos de datos en el tiempo.
* Pero debemos usarla con criterio: si el modelo es demasiado simple o demasiado complejo, puede **fallar**.
* NumPy y herramientas estadísticas nos permiten encontrar el equilibrio justo con funciones automáticas como `np.polyfit`.

---

