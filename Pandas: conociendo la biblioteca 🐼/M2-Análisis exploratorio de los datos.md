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
