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
# 📄 Formatos de Archivos Excel compatibles con `read_excel()` en Pandas

`read_excel()` no solo permite leer archivos `.xlsx`, sino también múltiples formatos comunes y de estándares abiertos.

---

## 🧰 Formatos de Microsoft Excel

### ✅ `.xlsx`

* **Formato predeterminado** desde Excel 2007.
* Basado en **XML (Extensible Markup Language)**.
* Compatible con herramientas como **Google Sheets**.
* 💡 Ideal para la mayoría de los usos.

---

### ✅ `.xls`

* Formato **antiguo**, usado hasta Excel 2003.
* Menos eficiente y menos seguro comparado con `.xlsx`.

---

### ✅ `.xlsm`

* Igual a `.xlsx`, pero permite **guardar macros** (scripts automáticos).
* ⚠️ Ideal para automatizaciones, pero puede presentar riesgos si contiene código malicioso.

---

### ✅ `.xlsb`

* Formato **binario** que permite leer y guardar archivos más rápidamente.
* ⚡ Recomendado para archivos de gran tamaño por su rapidez.

---

## 🌍 Formatos Abiertos Universales

Estos formatos están diseñados para ser **multiplataforma** y **multisoftware**:

### ✅ `.odf` (Open Document Format)

* Formato abierto estándar para documentos.

### ✅ `.ods` (Open Document Spreadsheet)

* Formato de hoja de cálculo usado por herramientas como LibreOffice, OpenOffice y Google Docs.
* Alternativa libre a `.xlsx`.

### ✅ `.odt` (Open Document Text)

* Formato para archivos de texto, no hojas de cálculo, pero también legible por algunas funciones de Pandas.

> Estos formatos están respaldados por **OASIS**, organización internacional que promueve estándares abiertos para documentos.

---

## 🛠️ Compatibilidad en Pandas

La función `pd.read_excel()` es capaz de manejar todos los formatos mencionados, siempre que tengas **las dependencias correctas instaladas** como:

* `openpyxl` → para `.xlsx`
* `xlrd` → para `.xls`
* `pyxlsb` → para `.xlsb`
* `odfpy` → para `.ods`, `.odf`, `.odt`

Puedes instalar estas bibliotecas con:

```bash
pip install openpyxl xlrd pyxlsb odfpy
```

---
# 📘 Parámetros de la Función `read_excel()`

La función `read_excel()` permite leer archivos Excel en múltiples formatos y ofrece parámetros para personalizar la lectura según tus necesidades.

---

## 🔧 Parámetros comunes de `read_excel()`

| Parámetro    | Descripción                                                              |
| ------------ | ------------------------------------------------------------------------ |
| `io`         | Ruta al archivo Excel que se desea leer.                                 |
| `sheet_name` | Nombre o índice de la hoja a leer. Si no se indica, lee la primera hoja. |
| `usecols`    | Permite seleccionar columnas específicas por nombre (`"A:D"`) o índice.  |
| `nrows`      | Limita el número de filas que se leen del archivo.                       |

---

## 🧪 Parámetros usados en clase

Durante la clase se usaron los siguientes parámetros:

* `sheet_name="Emisiones CO2"`

  > Especifica que se quiere leer la hoja **"Emisiones CO2"**.

* `usecols="A:D"`

  > Se seleccionan solo las columnas **de la A a la D**.

* `nrows=10`

  > Se leen únicamente las **primeras 10 filas** del archivo.

---

## 💡 Ejemplo de uso

```python
import pandas as pd

# Leer una hoja específica, con columnas y filas limitadas
intervalo_2 = pd.read_excel(
    "archivo.xlsx",
    sheet_name="Emisiones CO2",
    usecols="A:D",
    nrows=10
)
```

🔍 Esto carga en el DataFrame `intervalo_2`:

* Solo la hoja llamada **"Emisiones CO2"**
* Las columnas **A a D**
* Las **primeras 10 filas**

---
