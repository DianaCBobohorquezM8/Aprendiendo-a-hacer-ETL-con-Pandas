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
