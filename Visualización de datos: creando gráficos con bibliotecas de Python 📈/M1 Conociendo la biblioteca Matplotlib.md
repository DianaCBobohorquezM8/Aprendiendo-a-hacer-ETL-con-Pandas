# 📈 Módulo 1 : Conociendo la biblioteca Matplotlib 📈
---
# 📊 Extracción de una Serie de Datos en un DataFrame (Pandas)

---

## 🔹 1. Cargar y explorar los datos

```python
import pandas as pd

df = pd.read_csv("ruta/datos.csv")
```

* **`df.head()`** → muestra las primeras filas.
* **`df.shape`** → muestra el número de registros y columnas.
* **`df.info()`** → describe tipos de datos y valores nulos.

📌 En el ejemplo: 195 registros, 38 columnas y **sin valores nulos**.

---

## 🔹 2. Establecer un índice

```python
df.set_index('País', inplace=True)
```

* **Concepto:** El índice identifica de forma única cada fila.
* **`set_index()`** → convierte la columna `"País"` en índice.
* **`inplace=True`** → modifica el DataFrame original.

👉 Facilita la búsqueda y selección de datos por país.

---

## 🔹 3. Crear lista de años

```python
años = list(map(str, range(1980, 2014)))
```

* **`range(1980, 2014)`** → genera los números 1980–2013.
* **`map(str, ...)`** → convierte a strings (los nombres de columnas son cadenas).
* **`list(...)`** → lo convierte en lista.

📌 Resultado: `["1980", "1981", ..., "2013"]`.

---

## 🔹 4. Filtrar datos de Colombia

```python
Colombia = df.loc['Colombia', años]
```

* **`.loc[fila, columnas]`** → selecciona por nombre.
* `"Colombia"` → fila del país Colombia.
* `años` → columnas de 1980 a 2013.

📌 Resultado: un **Pandas Series** con los datos de inmigración de Colombia.

---

## 🔹 5. Convertir la Serie a DataFrame

```python
colDict = {
    "año": Colombia.index.to_list(),
    "inmigrantes": Colombia.values.to_list()
}

datos_col = pd.DataFrame(colDict)
```

* **Diccionario (`colDict`)**

  * `"año"` → lista de años (`Colombia.index.to_list()`).
  * `"inmigrantes"` → lista de valores (`Colombia.values.to_list()`).
* **`pd.DataFrame()`** → crea un DataFrame a partir del diccionario.

📌 Resultado: `datos_col` contiene dos columnas → **año** e **inmigrantes**.

---

## 🔹 6. Visualización

```python
datos_col.tail()
```

👉 Muestra los últimos registros del DataFrame creado.

---

## ✅ Resumen

1. **Carga** → `pd.read_csv()`.
2. **Exploración** → `head()`, `shape`, `info()`.
3. **Índice** → `set_index('País')`.
4. **Lista de años** → `list(map(str, range(...)))`.
5. **Serie de Colombia** → `df.loc['Colombia', años]`.
6. **Conversión** → `dict` → `pd.DataFrame()`.

---
# 📊 Relación entre el Plano Cartesiano y la Visualización de Datos

---

## 🔹 Analogía básica

* Un **mapa** ayuda a orientarse en el espacio real (calles, edificios, rutas).
* El **plano cartesiano** ayuda a orientarse en un **espacio de datos** (puntos, tendencias, relaciones).

👉 En ambos casos, la idea es **facilitar la comprensión** de información compleja para tomar decisiones.

---

## 🔹 Componentes principales del plano cartesiano

* **Eje X (abscisas)** → horizontal.
* **Eje Y (ordenadas)** → vertical.
* **Origen (0,0)** → punto de intersección.
* **Valores positivos** → derecha y arriba.
* **Valores negativos** → izquierda y abajo.

📌 Cada punto se representa con coordenadas `(x, y)` → su **ubicación exacta** en el plano.

---

## 🔹 Aplicación en la visualización de datos

* En un gráfico, **las coordenadas son los datos**:

  * `x` → variable independiente (ej. tiempo, categorías).
  * `y` → variable dependiente (ej. valores, frecuencias).
* Permite:

  * Identificar **patrones y tendencias**.
  * Comparar relaciones entre puntos/datos.
  * Detectar valores inusuales (outliers).

Ejemplo:

* Puntos `(2,5), (1,2), (0,-1), (-1,-4), (-2,-7)` muestran cómo los valores cambian a medida que se desplazan en los ejes.

---

## 🔹 Campos donde se usa

El plano cartesiano es una **herramienta universal** en:

* 📐 Matemáticas → representar funciones.
* ⚙️ Ingeniería → diagramas técnicos.
* 🔬 Física → trayectorias, fuerzas.
* 📈 Ciencia de datos → gráficos, visualización de resultados.

---
👉 En resumen:
El **plano cartesiano** es la base conceptual de casi todas las **visualizaciones de datos**, porque convierte números y relaciones en una forma **espacial y visual** fácil de interpretar.

---
# 📊 Creando el Primer Gráfico con Matplotlib

---

## 1️⃣ Importar Matplotlib

```python
import matplotlib.pyplot as plt
```

📌 **¿Qué hace?** Permite usar las funciones de Matplotlib para graficar.
🔎 **Analogía:** Es como abrir una caja de herramientas y ponerle una etiqueta `plt` para usarla fácilmente.

---

## 2️⃣ Crear el gráfico básico

```python
plt.plot(datos_col['año'], datos_col['inmigrantes'])
```

📌 **¿Qué hace?** Dibuja una línea entre las coordenadas del eje X (años) y Y (inmigrantes).
🔎 **Analogía:** `plt.plot` es el pincel 🎨 que dibuja la línea en el lienzo.

---

## 3️⃣ Ajustar los ticks del eje X

```python
plt.xticks([1980, 1985, 1990, 1995, 2000, 2005, 2010])
```

📌 **¿Qué hace?** Marca solo los años clave en el eje X.
🔎 **Analogía:** Es como resaltar con marcador fluorescente los años importantes en una regla.

---

## 4️⃣ Ajustar el tamaño de la figura

```python
plt.figure(figsize=(8, 4))
```

📌 **¿Qué hace?** Cambia el tamaño del gráfico a 8×4 pulgadas.
🔎 **Analogía:** Ajustar una ventana 🪟 para que el gráfico encaje perfecto.

---

## 5️⃣ Añadir títulos y etiquetas

```python
plt.title("Inmigración de colombianos hacia Canadá")
plt.xlabel("Año")
plt.ylabel("Número de inmigrantes")
```

📌 **¿Qué hace?** Da contexto al gráfico con un título y etiquetas.
🔎 **Analogía:** Como ponerle un rótulo a un cuadro en un museo 🖼️ para que todos entiendan lo que representa.

---

## 6️⃣ Mostrar el gráfico

```python
plt.show()
```

📌 **¿Qué hace?** Muestra el gráfico final en pantalla.
🔎 **Analogía:** Revelar la foto 📷: solo ves el resultado, no todo el proceso detrás.

---

## 7️⃣ Análisis de la tendencia

* 👀 **Observación visual:** identifica periodos de crecimiento, caída o estabilidad.
* 📈 **Picos y valles:** reconoce momentos de mayor y menor valor.

---

## 8️⃣ Almacenamiento de datos del gráfico

```python
grafico = plt.plot(datos_col['año'], datos_col['inmigrantes'])
```

📌 **¿Qué hace?** Guarda el gráfico en una variable para manipularlo después.
🔎 **Analogía:** Como guardar una copia digital de una pintura 🎨 para editarla más adelante.

---
