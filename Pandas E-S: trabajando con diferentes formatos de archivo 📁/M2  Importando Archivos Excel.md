# 🐼 Módulo  :  Importando Archivos Excel 📁
---

# 📗 Lectura de Archivos Excel

Aprender a importar y analizar archivos Excel es esencial cuando trabajamos con datos tabulares más complejos que los CSV. Aquí se detallan los conceptos fundamentales y herramientas clave.

---

## 🔹 ¿Qué es un archivo Excel?

* Formato: `.xlsx`
* Contiene **hojas de cálculo** organizadas en:

  * 🧱 **Filas**
  * 📊 **Columnas**
  * 📑 **Hojas múltiples**
* A diferencia del CSV, puede incluir:

  * Fórmulas, formatos de celda, gráficos, etc.

---

## 🧩 Cómo trabajar con archivos Excel en Google Colab

### ✅ Paso 1: Subir archivo

```python
from google.colab import files
uploaded = files.upload()
```

### ✅ Paso 2: Leer archivo con Pandas

```python
import pandas as pd

df = pd.read_excel('archivo.xlsx')
```

---

## 🛠️ Funciones y parámetros importantes

### 📘 `read_excel()`

Carga una hoja de Excel como un **DataFrame**.

---

### 🔸 `sheet_name`

* Selecciona la hoja a leer.
* Por defecto (`sheet_name=0`), carga la primera hoja.

```python
df = pd.read_excel('archivo.xlsx', sheet_name='ventas')
```

---

### 🔸 `usecols`

* Selecciona columnas específicas.
* Puede usarse con letras (`"A:D"`) o índices (`[0,1,2]`).

```python
df = pd.read_excel('archivo.xlsx', usecols='A:D')
```

---

### 🔸 `nrows`

* Limita el número de filas leídas.
* Útil para trabajar con archivos grandes.

```python
df = pd.read_excel('archivo.xlsx', nrows=10)
```

---

## 🔍 Exploración de hojas con `ExcelFile`

```python
archivo = pd.ExcelFile('archivo.xlsx')
archivo.sheet_names  # Lista con nombres de hojas
```

---

## 🔎 Métodos para explorar datos

| Método         | Descripción                    |
| -------------- | ------------------------------ |
| `df.head(n)`   | Muestra las primeras `n` filas |
| `df.tail(n)`   | Muestra las últimas `n` filas  |
| `df.sample(n)` | Muestra `n` filas aleatorias   |

---

## ✅ Resumen práctico

| Parámetro / Método             | Función principal                  |
| ------------------------------ | ---------------------------------- |
| `read_excel()`                 | Leer archivos `.xlsx`              |
| `sheet_name`                   | Elegir hoja específica             |
| `usecols`                      | Seleccionar columnas               |
| `nrows`                        | Limitar filas leídas               |
| `ExcelFile`                    | Explorar hojas disponibles         |
| `head()`, `tail()`, `sample()` | Inspeccionar contenido rápidamente |

---
