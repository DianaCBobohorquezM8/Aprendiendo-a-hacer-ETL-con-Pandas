# 🐼 Módulo 1 : Conociendo la base de datos 
---

## 🧩 ¿Qué es Pandas?

Pandas es una **biblioteca de Python especializada en el manejo y análisis de datos estructurados**, como los que encuentras en hojas de cálculo o bases de datos.

> 📊 **Piensa en Pandas como una súper hoja de cálculo que puedes controlar con código.**

🔍 Se utiliza principalmente para:

* Limpieza y preparación de datos
* Análisis exploratorio de datos (EDA)
* Manipulación y transformación
* Integración con visualización (Matplotlib, Seaborn)
---
## 🧱 Estructuras Principales de Pandas

| Estructura  | Descripción                                 | Ejemplo visual              |
| ----------- | ------------------------------------------- | --------------------------- |
| `Series`    | Columna de datos (1D) con índice            | `0 → "Ene", 1 → "Feb", ...` |
| `DataFrame` | Tabla (2D) con filas y columnas etiquetadas | como una hoja de cálculo    |

---

## 📚 Conceptos clave

| Término                                  | Descripción                                                                                     |
| ---------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Base de datos**                        | Colección organizada de datos, que podemos explorar y analizar con Pandas.                      |
| **EDA (Análisis Exploratorio de Datos)** | Proceso para identificar patrones, anomalías, hipótesis, etc. mediante estadísticas y gráficos. |
| **Valores nulos**                        | Datos faltantes o desconocidos. Pandas ofrece funciones para gestionarlos.                      |
| **Limpieza de datos**                    | Corregir errores, inconsistencias o datos vacíos para asegurar calidad.                         |
| **Manipulación de datos**                | Transformar y reorganizar datos (filtrar, ordenar, agrupar, combinar, etc.).                    |
| **Visualización de datos**               | Crear gráficos y tablas para comunicar los hallazgos de forma visual.                           |

---

## 🛠️ ¿Por qué Pandas?

✅ Estructuras de datos de alto rendimiento   
✅ Sintaxis sencilla y potente  
✅ Fácil integración con otras bibliotecas como NumPy, Matplotlib, Seaborn  
✅ Ideal para análisis de datos en ciencia, negocio y machine learning  

---
## 🔍 Relación con NumPy

Pandas está construido sobre **NumPy**, lo que le permite ser rápido y eficiente con operaciones vectorizadas. A diferencia de los arrays de NumPy, los objetos de Pandas (como `DataFrame` y `Series`) permiten **etiquetas** para filas y columnas, lo que los hace más legibles y manejables para datos reales.

---
# 📦 Importar, leer y explorar datos con Pandas

## 📥 Importar la biblioteca Pandas 🐼

Para comenzar a trabajar con Pandas, es importante seguir la convención estándar:

```python
import pandas as pd
```

Esto permite usar `pd` como un alias corto para acceder a todas las funciones y estructuras de Pandas.

---

## 🌐 Cargar un archivo CSV desde una URL

### 🗂️ Paso a paso:

1. **Copiar la URL del archivo CSV** (por ejemplo, desde un Gist de GitHub).
2. **Leer el archivo con `pd.read_csv()`**.
3. **Especificar el separador adecuado (`sep=';'`)** si los valores están separados por punto y coma.

```python
url = 'https://mi-url-del-archivo.csv'
datos = pd.read_csv(url, sep=';')
```

---

## 📋 ¿Qué es un DataFrame?

Un **DataFrame** es la estructura de datos principal de Pandas:

* 📑 Bidimensional (filas y columnas)
* 🔣 Puede contener diferentes tipos de datos: números, texto, fechas…
* 📊 Ideal para representar tablas como las de Excel o bases de datos.

---

## 👀 Explorar los datos

| Comando           | Función                                                        |
| ----------------- | -------------------------------------------------------------- |
| `datos.head(n)`   | Muestra las primeras `n` filas. Por defecto, muestra 5.        |
| `datos.tail(n)`   | Muestra las últimas `n` filas.                                 |
| `datos.sample(n)` | Muestra una muestra aleatoria de `n` filas del DataFrame.      |
| `type(datos)`     | Verifica que la estructura de datos sea un `pandas.DataFrame`. |

### 🔍 Ejemplos:

```python
print(datos.head())        # Primeras 5 filas
print(datos.head(10))      # Primeras 10 filas
print(datos.tail(3))       # Últimas 3 filas
print(datos.sample(5))     # 5 filas aleatorias
print(type(datos))         # Verifica tipo: <class 'pandas.core.frame.DataFrame'>
```

---

## 📄 ¿Qué es un archivo CSV?

**CSV** (Comma Separated Values) es un formato de archivo de texto donde los valores están separados por:

* Comas `,` (formato estándar)
* Punto y coma `;` (muy común en archivos de Europa o exportados desde Excel)

💡 Pandas permite ajustar esto fácilmente con el argumento `sep`.

---
# 🧾 Importación de datos desde diferentes formatos en Pandas

Pandas ofrece diversas funciones para **importar y exportar** datos en distintos formatos. Esto permite trabajar con múltiples fuentes de datos en proyectos de análisis, ciencia de datos y machine learning. ⚙️📊

---

## 📥 Funciones principales de importación

A continuación se presentan las funciones más comunes para importar datos en Pandas:

| 📂 Formato de archivo | 🛠️ Función de Pandas | 📄 Descripción |
|------------------------|----------------------|----------------|
| **CSV** (`.csv`)       | `read_csv()`         | Archivos de texto separados por comas. Ideal para datos tabulares. |
| **Excel** (`.xls`, `.xlsx`) | `read_excel()`     | Archivos de hojas de cálculo de Excel. Permite especificar la hoja. |
| **JSON** (`.json`)     | `read_json()`        | Archivos con datos estructurados como objetos de JavaScript. |
| **HTML** (`.html`)     | `read_html()`        | Extrae tablas desde páginas web con estructura HTML. |
| **Bases de Datos SQL** | `read_sql()`         | Permite leer desde bases de datos relacionales usando consultas SQL. |

---

## 🔎 Explicaciones y ejemplos

### 📄 `read_csv()`

**Descripción**: Lee archivos de texto donde los valores están separados por comas.  
💡 Personalizable con argumentos como `delimiter`, `header`, `encoding`, etc.

```python
import pandas as pd

df = pd.read_csv("archivo.csv", delimiter=",", encoding="utf-8")
````

---

### 📊 `read_excel()`

**Descripción**: Carga hojas de cálculo de Excel (`.xls` o `.xlsx`).
Puedes indicar la hoja con `sheet_name`.

```python
df = pd.read_excel("datos.xlsx", sheet_name="Ventas")
```

---

### 🧾 `read_json()`

**Descripción**: Importa archivos `.json`, útiles cuando los datos están en estructuras jerárquicas.

```python
df = pd.read_json("datos.json")
```

---

### 🌐 `read_html()`

**Descripción**: Extrae automáticamente todas las tablas de una página web (requiere librerías como `lxml` o `html5lib`).

```python
url = "https://es.wikipedia.org/wiki/Anexo:Países_por_PIB"
tablas = pd.read_html(url)
df = tablas[0]
```

📦 Instala los paquetes necesarios:

```bash
pip install lxml html5lib
```

---

### 🗄️ `read_sql()`

**Descripción**: Conecta con bases de datos como **MySQL**, **PostgreSQL**, **SQLite**, entre otras.

```python
import sqlite3

conn = sqlite3.connect("mi_base.db")
df = pd.read_sql("SELECT * FROM clientes", conn)
conn.close()
```
---
# 🧮 Estructuras de Datos en Pandas: `Series` y `DataFrame`

Cuando trabajas con Pandas, es fundamental entender sus dos estructuras de datos principales: **Serie** y **DataFrame**. Ambas te permiten organizar y analizar datos de manera eficiente en Python.

---

## 🔹 ¿Qué es una Serie?

Una **Serie** es como una **columna individual** de una hoja de cálculo. Se trata de una estructura unidimensional con etiquetas (índices) y datos del mismo tipo.

```python
import pandas as pd

serie = pd.Series([10, 20, 30], name="Edad")
print(serie)
````

✅ **Salida**:

```
0    10
1    20
2    30
Name: Edad, dtype: int64
```

🧠 **Características de una Serie**:

* Contiene **valores** y **etiquetas de índice**
* Es unidimensional
* Puede almacenar cualquier tipo de datos (números, texto, fechas, etc.)

---

## 🔸 ¿Qué es un DataFrame?

Un **DataFrame** es como una **hoja de cálculo completa**: una tabla compuesta por varias **Series** (columnas), todas compartiendo el mismo índice (las filas).

```python
data = {
    "Nombre": ["Ana", "Luis", "Camila"],
    "Edad": [25, 30, 22],
    "Ciudad": ["Bogotá", "Medellín", "Cali"]
}
df = pd.DataFrame(data)
print(df)
```

✅ **Salida**:

|   | Nombre | Edad | Ciudad   |
| - | ------ | ---- | -------- |
| 0 | Ana    | 25   | Bogotá   |
| 1 | Luis   | 30   | Medellín |
| 2 | Camila | 22   | Cali     |

🧠 **Características de un DataFrame**:

* Estructura **bidimensional**
* Cada columna es una Serie
* Índice compartido entre columnas

---

## 📋 Comparación rápida

| 📘 Característica | 🟦 Serie             | 🟨 DataFrame                 |
| ----------------- | -------------------- | ---------------------------- |
| Dimensiones       | 1D                   | 2D                           |
| Contenido         | Una sola columna     | Varias columnas              |
| Índice            | Individual           | Compartido entre columnas    |
| Similar a         | Una columna de Excel | Una hoja de cálculo completa |

---

## 🔍 `datos.dtypes`: Tipos de datos por columna

Este atributo devuelve el tipo de dato de cada columna del DataFrame:
`int64` (enteros), `float64` (decimales), `object` (texto), `datetime64`, etc.

```python
print(datos.dtypes)
```

✅ **Ejemplo de salida**:

```
tipo           object
colonia        object
habitaciones     int64
garajes         int64
suites          int64
area            int64
valor         float64
condominio    float64
impuesto      float64
dtype: object
```

🍎 **Analogía**:
Imagina que tienes una caja con diferentes tipos de frutas:

* Manzanas 🍎 → enteros (`int64`)
* Naranjas cortadas 🍊 → decimales (`float64`)
* Etiquetas con nombres 🏷️ → texto (`object`)

`datos.dtypes` te diría qué tipo hay en cada compartimento.

---

## 📈 `datos.describe()`: Estadísticas Descriptivas

Este método proporciona un resumen estadístico de las **columnas numéricas**:

* **count**: número de datos
* **mean**: media
* **std**: desviación estándar
* **min / max**: valor mínimo y máximo
* **25% / 50% / 75%**: cuartiles

```python
print(datos.describe())
```

✅ **Ejemplo de salida**:

|           | habitaciones | garajes | suites  | area    | valor   | condominio | impuesto |
| --------- | ------------ | ------- | ------- | ------- | ------- | ---------- | -------- |
| **count** | 25121.0      | 25121.0 | 25121.0 | 25121.0 | 25121.0 | 25121.0    | 25121.0  |
| **mean**  | 2.50         | 1.06    | 1.03    | 150.5   | 6654.1  | 540.48     | 1245.8   |
| **std**   | 1.17         | 0.82    | 1.16    | 374.7   | 8429.7  | 4588.17    | 3410.8   |
| **min**   | 1.0          | 0.0     | 0.0     | 10.0    | 500.0   | 0.0        | 0.0      |
| **25%**   | 2.0          | 1.0     | 0.0     | 58.0    | 2000.0  | 0.0        | 0.0      |

🍊 **Analogía**:
Es como obtener un reporte estadístico de una caja de frutas:
Te dice cuántas hay, el peso promedio, cuál es la más liviana y la más pesada, etc.

---

