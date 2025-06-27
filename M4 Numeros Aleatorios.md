## 🎲 Generación de Números Aleatorios

### 📌 ¿Por qué usar números aleatorios?

Generar valores aleatorios es una práctica muy útil en **ciencia de datos, simulaciones, pruebas de modelos** y visualización. Con NumPy, puedes generar tanto **enteros** como **números decimales aleatorios**, almacenarlos y analizarlos fácilmente.

---

## 🔢 Funciones de generación aleatoria

### 1. **`np.random.randint()`**

Genera números enteros aleatorios en un rango definido.

```python
import numpy as np

enteros = np.random.randint(40, 100, 10)
print(enteros)  # Ejemplo: [72 64 91 45 88 40 93 70 69 54]
```

* **Primer parámetro**: valor mínimo (incluido).
* **Segundo parámetro**: valor máximo (excluido).
* **Tercer parámetro**: cantidad de números que deseas generar.

---

### 2. **`np.random.uniform()`**

Genera números de punto flotante (decimales) aleatorios.

```python
decimales = np.random.uniform(0.1, 0.9, 5)
print(decimales)  # Ejemplo: [0.26 0.77 0.51 0.31 0.48]
```

* Perfecto para explorar valores **continuos** en un intervalo.

---

## 📊 Almacenamiento en `np.array`

Los resultados de `randint()` y `uniform()` se pueden guardar directamente en arrays de NumPy:

```python
pendientes = np.random.uniform(0.5, 2.0, 100)
```

Esto permite **analizar, visualizar y comparar** los valores fácilmente, por ejemplo usando gráficos o métricas como la norma.

---

## 🔁 Aplicación práctica: Búsqueda de la mejor pendiente

Cuando queremos encontrar la mejor pendiente $a$ para una línea $y = ax + b$, podemos generar valores aleatorios de $a$, calcular el error (norma) y ver cuál se ajusta mejor a los datos reales:

```python
x = np.arange(1, 13)
datos_reales = np.array([80, 82, 85, 88, 90, 91, 94, 95, 98, 100, 102, 105])
interseccion = 75

errores = []
pendientes = np.random.uniform(0.5, 2.0, 100)

for a in pendientes:
    y_estimado = a * x + interseccion
    error = np.linalg.norm(datos_reales - y_estimado)
    errores.append(error)
```

---

### 📏 ¿Qué es `np.linalg.norm()`?

* Calcula la **norma euclidiana** (longitud o magnitud) entre dos arrays.
* Se usa para **medir qué tan diferente es una predicción respecto a los datos reales**.

---

### ➕ ¿Y `np.append()`?

* Se utiliza para **agregar elementos a un array**.

```python
norma = np.array([])
for a in pendientes:
    error = np.linalg.norm(datos_reales - (a * x + interseccion))
    norma = np.append(norma, error)
```

---

## 🔐 Control de la Aleatoriedad: Semillas

Cada vez que generas números aleatorios, los resultados cambian.
Pero si quieres **reproducir los mismos valores**, puedes **fijar una semilla**:

```python
np.random.seed(42)
```

Esto es útil para:

* Repetir experimentos.
* Comparar resultados.
* Tener documentación reproducible.

---

## 🧠 Conclusión

| Concepto            | Explicación clave                                                             |
| ------------------- | ----------------------------------------------------------------------------- |
| `np.random.randint` | Números enteros aleatorios en un rango.                                       |
| `np.random.uniform` | Números decimales aleatorios.                                                 |
| `np.array()`        | Permite guardar y procesar esos valores.                                      |
| `np.linalg.norm()`  | Calcula la diferencia entre los datos reales y estimados (distancia o error). |
| `np.append()`       | Agrega valores a un array existente.                                          |
| `np.random.seed()`  | Controla la aleatoriedad para resultados consistentes.                        |


## 🎲 Generación de Pendientes Aleatorias para Modelar Precios

Cuando queremos ajustar una **línea recta** a un conjunto de datos, una estrategia útil es **probar muchas pendientes diferentes** (valores de $a$ en la ecuación $y = ax + b$) y medir cuál de ellas se ajusta mejor. NumPy nos permite hacer esto con generación de números aleatorios, cálculo de normas, y almacenamiento de errores para su posterior análisis.

### 📌 Ejemplo completo: Búsqueda de la mejor pendiente

```python
import numpy as np

# Datos reales de precios de manzanas en Moscú
Moscu = np.array([80, 82, 85, 88, 90, 91, 94, 95, 98, 100, 102, 105])
x = np.arange(1, 13)  # Meses del año
b = 75  # Valor fijo para la intersección con el eje Y

# Generar 100 pendientes aleatorias entre 0.5 y 2.0
pendientes = np.random.uniform(0.5, 2.0, 100)

# Crear un array vacío para almacenar las normas (errores)
norma = np.array([])

# Calcular la diferencia entre los datos reales y cada línea generada
for i in range(100):
    y_estimado = pendientes[i] * x + b
    error = np.linalg.norm(Moscu - y_estimado)
    norma = np.append(norma, error)
```

---

### 🧠 ¿Qué está pasando aquí?

| Línea de código                                 | Explicación                                                                    |
| ----------------------------------------------- | ------------------------------------------------------------------------------ |
| `pendientes = np.random.uniform(0.5, 2.0, 100)` | Genera 100 pendientes aleatorias para probar.                                  |
| `norma = np.array([])`                          | Inicializa un array vacío donde guardaremos los errores (normas).              |
| `for i in range(100):`                          | Recorremos las 100 pendientes generadas.                                       |
| `y_estimado = pendientes[i] * x + b`            | Calculamos los valores estimados de precios con esa pendiente.                 |
| `np.linalg.norm(Moscu - y_estimado)`            | Calculamos la diferencia (distancia) entre los valores reales y los estimados. |
| `np.append(norma, error)`                       | Guardamos ese error en el array `norma`.                                       |

---

### 📈 ¿Qué puedes hacer luego con `norma`?

* 📊 **Visualizar los errores**: por ejemplo, usando `plt.plot(pendientes, norma)` para ver qué pendiente tiene el menor error.
* 🏆 **Encontrar la mejor pendiente**:

```python
mejor_indice = np.argmin(norma)
mejor_pendiente = pendientes[mejor_indice]
print(f"La mejor pendiente encontrada es: {mejor_pendiente}")
```

---

### 🔐 Reproducibilidad

Si quieres que los valores aleatorios siempre sean los mismos (por ejemplo, al compartir tu código), fija la semilla antes de generar los números aleatorios:

```python
np.random.seed(42)
```
---

## 🎲 Números Pseudoaleatorios y Semillas en NumPy

### 🔢 ¿Qué son los números *pseudoaleatorios*?

En realidad, los números generados por `NumPy` no son verdaderamente aleatorios. Se les llama **números pseudoaleatorios** porque:

* Se generan usando **algoritmos deterministas**.
* Parecen aleatorios, pero **siempre son los mismos si se usa la misma semilla (seed)**.

Esto significa que puedes tener resultados **reproducibles**, lo cual es muy útil en programación, ciencia de datos y machine learning.

---

### 🌱 `np.random.seed()`: Fijando el estado de aleatoriedad

```python
np.random.seed(42)
```

Esta línea establece un **estado inicial (seed)** para el generador de números aleatorios de NumPy. Esto asegura que:

✅ Cada vez que ejecutes el código con esa semilla, obtendrás los **mismos números aleatorios**.

---

### 🧪 Ejemplo práctico

```python
import numpy as np

np.random.seed(42)
numeros = np.random.randint(0, 100, 5)
print(numeros)  # Siempre imprimirá: [51 92 14 71 60]
```

Ahora, si ejecutas este código varias veces, siempre obtendrás exactamente los mismos números. Si **no pones la semilla**, los valores cambiarán en cada ejecución.

---

### 🧠 ¿Por qué es importante usar una semilla?

| Situación                 | Ventaja de usar `seed()`                                              |
| ------------------------- | --------------------------------------------------------------------- |
| Entrenamiento de modelos  | Puedes reproducir los mismos resultados cada vez.                     |
| Pruebas de código         | Puedes verificar si un algoritmo funciona igual con los mismos datos. |
| Comparación de soluciones | Puedes comparar métodos usando la misma secuencia aleatoria.          |

---

### ⚠️ Recomendación importante

Coloca siempre `np.random.seed()` **justo antes** de generar los números aleatorios para garantizar la coherencia:

```python
np.random.seed(0)
pendientes = np.random.uniform(0.5, 2.0, 100)
```

Si defines la semilla en una celda diferente (como en Jupyter Notebooks), puede no tener efecto si luego generas números aleatorios más adelante.

---

### 📌 Resumen

* NumPy genera **números pseudoaleatorios**, no verdaderamente aleatorios.
* Usa `np.random.seed(valor)` para fijar la **semilla** del generador.
* Esto permite que tu código sea **reproducible y verificable**.
* Es muy útil en simulaciones, pruebas, aprendizaje automático, y cualquier tarea que requiera **consistencia**.

---

