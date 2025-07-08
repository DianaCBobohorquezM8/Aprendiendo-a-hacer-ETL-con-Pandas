# 🐼 Módulo 2 : Análisis exploratorio de los datos
---

# 🔍 Análisis Exploratorio de Datos (AED) en Pandas

El **Análisis Exploratorio de Datos (AED)** es un proceso clave para comprender y preparar nuestros datos antes de aplicar modelos o sacar conclusiones. 

---

## 🧠 ¿Qué es el AED?

El **Análisis Exploratorio de Datos** consiste en:

- 📋 Identificar tipos de datos
- 🔎 Detectar valores faltantes o atípicos
- 📊 Explorar distribuciones y tendencias
- 🧮 Calcular estadísticas descriptivas
- 🎨 Visualizar información para obtener insights

---

## 📦 Agrupamiento con `groupby()`

La función `groupby()` en Pandas permite **agrupar filas** por una o más columnas y aplicar funciones estadísticas a cada grupo.

### ✅ Ejemplo:

```python
grupo = datos.groupby("tipo")["valor"]
promedio = grupo.mean()
print(promedio)
````

🎯 Esto calcula el **valor promedio** por tipo de propiedad.

---

## 📊 Promedio por tipo de propiedad + Visualización

Para ver estos promedios de forma visual, puedes usar `plot()` con un gráfico de barras horizontal:

```python
promedio.sort_values().plot(
    kind="barh", 
    figsize=(8, 5), 
    color="skyblue", 
    title="Promedio de alquiler por tipo de propiedad"
)
```

📌 Aquí se usa:

* `kind="barh"` → gráfico de barras horizontal
* `figsize=(8,5)` → tamaño del gráfico
* `color="skyblue"` → color personalizado

---

## 📈 Porcentaje por tipo de propiedad

También puedes calcular el porcentaje que representa cada tipo de propiedad respecto al total:

```python
porcentaje = datos["tipo"].value_counts(normalize=True) * 100
print(porcentaje)
```

💡 `normalize=True` convierte el conteo en proporciones.

---

## 🎨 Visualización del porcentaje

```python
porcentaje.plot(
    kind="bar", 
    figsize=(8, 4), 
    color="coral", 
    title="Distribución porcentual por tipo de propiedad"
)
```

---

## 📚 Ordenación con `sort_values()`

La función `sort_values()` permite **ordenar** un DataFrame o Serie de acuerdo con valores de una o varias columnas.

### 🛠️ Uso básico

```python
df_ordenado = datos.sort_values(by="valor")
```

* `by` → columna a ordenar
* `ascending=True` (por defecto) → orden de menor a mayor

### 🔄 Orden descendente

```python
df_desc = datos.sort_values(by="valor", ascending=False)
```

---

### 📊 Ordenar por múltiples columnas

```python
df_multi = datos.sort_values(by=["ciudad", "valor"], ascending=[True, False])
```

✅ Primero ordena por `ciudad` (A-Z), y luego por `valor` (mayor a menor).

---

### ❓ ¿Qué pasa con los valores nulos?

Puedes decidir si se muestran primero o al final con `na_position`:

```python
datos.sort_values(by="valor", na_position="first")
```

---

### 🔄 ¿Modificar original o crear nuevo?

| Argumento       | Descripción                                 |
| --------------- | ------------------------------------------- |
| `inplace=False` | Crea un nuevo DataFrame (valor por defecto) |
| `inplace=True`  | Modifica el DataFrame original directamente |

```python
datos.sort_values(by="valor", inplace=True)
```
---
# 🔄 Agrupación y Agregación con `groupby()` en Pandas

La función `groupby()` es una herramienta esencial en Pandas para **agrupar datos** según uno o más criterios, y aplicar operaciones estadísticas a cada grupo. Junto con ella, el parámetro `numeric_only=True` es muy útil para evitar errores cuando se mezclan tipos de datos.

---

## 🧠 ¿Qué hace `groupby()`?

Permite dividir un **DataFrame** en **grupos** con base en:
- Una o varias columnas (criterios de agrupación)
- El índice del DataFrame (si se desea)

Luego, puedes aplicar operaciones como:
- `sum()`
- `mean()`
- `count()`
- `std()`
- O funciones personalizadas con `.apply()` o `.agg()`

---

## 🔧 Parámetros principales de `groupby()`

| Parámetro   | Tipo        | Descripción |
|-------------|-------------|-------------|
| `by`        | str o list  | Columna(s) por las que agrupar |
| `axis`      | int         | Eje de agrupación: `0` para filas (por defecto), `1` para columnas |
| `sort`      | bool        | Ordenar grupos por los valores del `by`. Por defecto `True` |
| `dropna`    | bool        | Eliminar valores nulos (`NaN`) antes de agrupar. Por defecto `True` |

---

## ✅ Ejemplo básico de `groupby()`

```python
agrupado = datos.groupby("tipo")["valor"].mean()
print(agrupado)
````

🔍 Esto calcula el **promedio** de la columna `valor`, agrupado por cada tipo de propiedad (`tipo`).

---

## 🧮 ¿Qué es `numeric_only=True`?

Este parámetro aparece en funciones como `mean()`, `sum()`, `median()`, etc., y permite aplicar operaciones **solo sobre columnas numéricas**.

### 🛑 ¿Por qué es útil?

Cuando tu DataFrame tiene columnas no numéricas (texto, booleanos, fechas...), estas pueden causar errores o resultados incorrectos al aplicar funciones matemáticas.

---

## 🎯 Ejemplo sin y con `numeric_only=True`

### ⚠️ Sin usar `numeric_only`

```python
datos.groupby("tipo").mean()
```

Este comando **puede fallar** o mostrar advertencias si hay columnas no numéricas.

---

### ✅ Usando `numeric_only=True`

```python
datos.groupby("tipo").mean(numeric_only=True)
```

Ahora, solo se calcularán promedios sobre columnas con tipos `int`, `float`, etc.

---

## 📋 Comparación rápida

| Situación                         | ¿Qué pasa?                         | Solución segura       |
| --------------------------------- | ---------------------------------- | --------------------- |
| `groupby().sum()` con texto       | Error o ignora columnas no válidas | ✅ `numeric_only=True` |
| DataFrame mixto (texto + números) | Resultados inesperados sin filtrar | ✅ `numeric_only=True` |

---

## 🧪 Ejemplo completo

```python
agrupado = datos.groupby("tipo").mean(numeric_only=True)

agrupado.sort_values(by="valor").plot(
    kind="barh",
    figsize=(8,5),
    color="green",
    title="Promedio de variables numéricas por tipo"
)
```

🎨 Aquí agrupamos, promediamos solo valores numéricos, ordenamos y visualizamos.

---
# 📊 Análisis de Columnas, Filtrado y Visualización

## 🔢 `unique()`: Valores únicos de una columna

Este método devuelve los valores únicos encontrados en una columna de un DataFrame.

### ✅ Ejemplo:

```python
datos["tipo"].unique()
````

🧠 **Usos comunes**:

* Identificar categorías en columnas como `tipo`, `ciudad`, `estado`.
* Detectar errores o duplicados en etiquetas.

---

## 🔢 `value_counts()`: Conteo de valores

Este método cuenta cuántas veces aparece cada valor único en una columna.

### ✅ Ejemplo:

```python
datos["tipo"].value_counts()
```

| Tipo de propiedad | Conteo |
| ----------------- | ------ |
| Apartamento       | 9800   |
| Casa              | 6400   |
| Comercial         | 1500   |

---

### 🎯 Con `normalize=True`: Porcentajes

Agrega el parámetro `normalize=True` para obtener proporciones en lugar de conteos:

```python
datos["tipo"].value_counts(normalize=True) * 100
```

✅ **Resultado de ejemplo**:

| Tipo de propiedad | Porcentaje (%) |
| ----------------- | -------------- |
| Apartamento       | 48.9%          |
| Casa              | 32.0%          |
| Comercial         | 7.5%           |

---

## 🔍 `query()`: Filtrar con condiciones

Permite seleccionar filas según una condición, de forma legible y elegante.

### ✅ Ejemplo:

```python
inmuebles_residenciales = datos.query("tipo not in @tipos_comerciales")
```

📌 Donde `tipos_comerciales` es una lista como:

```python
tipos_comerciales = ["Comercial", "Industria"]
```

---

### 💡 Sintaxis especial con `query()`

| Elemento               | Función                                       |
| ---------------------- | --------------------------------------------- |
| `@variable`            | Usar una variable externa dentro del query    |
| `not in`               | Filtrar valores que **no están** en una lista |
| `"columna == 'valor'"` | Condición directa de comparación              |

---

### 📋 Verificación con `head()`

Después de filtrar, puedes verificar el resultado con:

```python
inmuebles_residenciales.head()
```

---

## 📈 Visualización con `plot()`

El método `plot()` te permite crear gráficos directamente desde tus datos.

### ✅ Ejemplo:

```python
porcentajes = datos["tipo"].value_counts(normalize=True) * 100

porcentajes.plot(
    kind="bar", 
    figsize=(12, 8), 
    color="green", 
    xlabel="Tipos de Propiedad", 
    ylabel="Porcentajes",
    title="Distribución de tipos de propiedades"
)
```

---

## 🎨 Parámetros comunes de `plot()`

| Parámetro         | Descripción                         |
| ----------------- | ----------------------------------- |
| `kind='bar'`      | Tipo de gráfico (barras verticales) |
| `figsize=(12, 8)` | Tamaño del gráfico en pulgadas      |
| `color='green'`   | Color de las barras                 |
| `xlabel='...'`    | Etiqueta del eje X                  |
| `ylabel='...'`    | Etiqueta del eje Y                  |
| `title='...'`     | Título del gráfico                  |

---
# 🏷️ Cambiar los nombres de columnas

Cuando trabajas con datos en Pandas, es común necesitar **renombrar columnas** para que tengan nombres más significativos, legibles o consistentes con tus análisis.

---

## 🔁 Método 1: Usando `rename()`

Este método te permite **cambiar uno o varios nombres de columnas**, especificando un diccionario donde:

- La **clave** es el nombre actual de la columna
- El **valor** es el nuevo nombre que deseas asignar

### ✅ Sintaxis:

```python
df.rename(columns={'columna_vieja': 'columna_nueva'}, inplace=True)
````

### 📌 Ejemplo práctico:

```python
# Crear un DataFrame de ejemplo
import pandas as pd

data = {'columna_A': [1, 2, 3],
        'columna_B': [4, 5, 6],
        'columna_C': [7, 8, 9]}
df = pd.DataFrame(data)

# Cambiar nombres de varias columnas
df.rename(columns={
    'columna_A': 'nueva_columna_A',
    'columna_B': 'nueva_columna_B',
    'columna_C': 'nueva_columna_C'
}, inplace=True)

print(df)
```

✅ **Resultado:**

|   | nueva\_columna\_A | nueva\_columna\_B | nueva\_columna\_C |
| - | ----------------- | ----------------- | ----------------- |
| 0 | 1                 | 4                 | 7                 |
| 1 | 2                 | 5                 | 8                 |
| 2 | 3                 | 6                 | 9                 |

---

## 📝 ¿Qué hace `inplace=True`?

* Si lo incluyes (`inplace=True`), el cambio se aplica **directamente** sobre el DataFrame.
* Si lo omites, se devuelve un **nuevo DataFrame** con los cambios.

---

## 🔁 Método 2: Usando `.columns` para renombrar todas las columnas

Si quieres cambiar **todos los nombres de columnas a la vez**, puedes reasignar una nueva lista con los nombres deseados.

### ✅ Ejemplo:

```python
df.columns = ['ID', 'Edad', 'Ciudad']
```

🎯 Muy útil cuando estás cargando archivos con nombres genéricos o en otro idioma.

---

## 💡 Caso común: Renombrar una columna después de agrupar

Imagina que haces esto:

```python
df_ejemplo = df['Tipo'].value_counts(normalize=True).to_frame().sort_values('Tipo')
```

El resultado tiene una sola columna llamada `"Tipo"` que contiene los porcentajes. Si deseas cambiar su nombre a `"Porcentajes"`:

```python
df_ejemplo.rename(columns={'Tipo': 'Porcentajes'}, inplace=True)
```

---

## 🧠 Recuerda

| Situación                        | Método recomendado         |
| -------------------------------- | -------------------------- |
| Renombrar 1 o varias columnas    | `df.rename(columns={...})` |
| Renombrar **todas** las columnas | `df.columns = [...]`       |

---



