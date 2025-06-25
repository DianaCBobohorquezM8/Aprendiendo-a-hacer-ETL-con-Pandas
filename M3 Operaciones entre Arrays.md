
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


