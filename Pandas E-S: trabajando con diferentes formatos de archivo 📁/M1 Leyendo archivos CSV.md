# 🐼 Módulo 1 : Leyendo archivos CSV   📁
---
# 📁 Leer Archivos CSV 

Una cadena de supermercados necesita identificar a sus **mejores clientes** para ofrecerles un descuento especial. Para ello, se trabaja con una **base de datos de clientes en formato CSV**.

---

## 📌 ¿Qué es un archivo CSV?

* **CSV** significa *Comma-Separated Values* o *valores separados por comas*.
* Es un archivo de texto donde **cada línea representa una fila** y **cada campo está separado por comas**.

  Es la función principal de Pandas para leer datos desde un archivo CSV y convertirlos en un DataFrame, que es una estructura de datos tabular muy útil para el análisis.
---

## 🧠 ¿Qué hace Pandas al leer un CSV?

Cuando usamos `pd.read_csv()`:

1. Abre el archivo.
2. Lee su contenido línea por línea.
3. Divide cada línea por comas.
4. Usa la **primera línea como nombres de columnas**.
5. Crea un **DataFrame**, que es una tabla manipulable.
6. Detecta automáticamente el tipo de dato de cada columna.

---

## 📊 Ejemplo de archivo `ejemplo.csv`

```
nombre,edad,ciudad
Juan,25,Madrid
Maria,30,Barcelona
Pedro,22,Valencia
```

### Resultado en Pandas:

| nombre | edad | ciudad    |
| ------ | ---- | --------- |
| Juan   | 25   | Madrid    |
| Maria  | 30   | Barcelona |
| Pedro  | 22   | Valencia  |

---

## ✅ Pasos para Leer un CSV en Google Colab

### 🧩 Paso 1: Importar Pandas

```python
import pandas as pd
```

> Asigna el alias `pd`, una convención estándar para Pandas.

---

### 🧩 Paso 2: Subir el archivo CSV

En Google Colab:

```python
from google.colab import files
uploaded = files.upload()
```

> Selecciona el archivo CSV desde tu PC cuando aparezca el cuadro de carga.

---

### 🧩 Paso 3: Leer el archivo con `read_csv()`

```python
datos = pd.read_csv('nombre_del_archivo.csv')
```

> Asegúrate de que el nombre del archivo esté entre comillas y coincida exactamente.

---

### 🧩 Paso 4: Inspeccionar el contenido

```python
datos.head()
```

> Muestra las **primeras 5 filas** del DataFrame para verificar que se haya leído correctamente.

---
# ⚙️ Parámetros clave de `pd.read_csv()`

La función `read_csv()` de **Pandas** permite personalizar cómo se leen los archivos CSV. A continuación, se describen los **parámetros más útiles**:

---

## 🔸 `sep` — Separador de campos

* Define el carácter que separa los campos del archivo.
* **Por defecto**: coma (`,`).
* Útil si el archivo usa punto y coma (`;`), tabulación (`\t`) u otro separador.

### ✅ Ejemplo:

```python
import pandas as pd
# Leer un archivo separado por punto y coma
df = pd.read_csv('archivo.csv', sep=';')
```

---

## 🔸 `nrows` — Número de filas a leer

* Permite leer solo un número limitado de filas.
* Muy útil para obtener una muestra cuando el archivo es muy grande.

### ✅ Ejemplo:

```python
import pandas as pd
# Leer solo las primeras 100 filas
df = pd.read_csv('archivo.csv', nrows=100)
```

---

## 🔸 `usecols` — Columnas específicas a leer

* Permite seleccionar solo algunas columnas del archivo.
* Se puede usar con **nombres de columna** o **índices de posición**.
* Ayuda a reducir uso de memoria y enfocarse en los datos relevantes.

### ✅ Ejemplo (por nombre):

```python
import pandas as pd
# Leer solo las columnas 'nombre', 'edad' y 'ciudad'
df = pd.read_csv('archivo.csv', usecols=['nombre', 'edad', 'ciudad'])
```

### ✅ Ejemplo (por posición):

```python
import pandas as pd
# Leer solo las columnas en las posiciones 0, 2 y 5
df = pd.read_csv('archivo.csv', usecols=[0, 2, 5])
```

---
