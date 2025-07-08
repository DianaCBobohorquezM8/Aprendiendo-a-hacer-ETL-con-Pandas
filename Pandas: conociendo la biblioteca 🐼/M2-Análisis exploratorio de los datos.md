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
