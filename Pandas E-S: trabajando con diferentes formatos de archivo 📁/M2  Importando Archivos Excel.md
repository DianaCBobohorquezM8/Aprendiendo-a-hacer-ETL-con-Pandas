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
# 📤 Escribiendo Archivos Excel

Pandas ofrece el método `to_excel()` para guardar tus datos en un archivo Excel `.xlsx`.

---

## 🧾 Exportar un DataFrame a Excel

```python
df.to_excel('nombre_archivo.xlsx', index=False)
```

### 🔹 Detalles:

* `to_excel()` → Método para **guardar un DataFrame en formato Excel**.
* `'nombre_archivo.xlsx'` → Especifica el **nombre del archivo de salida** (con extensión `.xlsx`).
* `index=False` → **Evita guardar la columna del índice** del DataFrame en el archivo (es opcional, pero recomendable si no necesitas el índice).

---

## 📥 Leer un archivo de Excel

```python
df = pd.read_excel('nombre_archivo.xlsx')
```

* Se usa `read_excel()` para cargar nuevamente el archivo `.xlsx` en un **DataFrame**.

---

## ✅ Verificación de la Exportación

Después de guardar un archivo:

1. **Leer el archivo** con `read_excel()`.
2. **Usar `.head()`, `.info()` o `.shape()`** para asegurarte de que los datos están completos y bien estructurados.

```python
df_verificacion = pd.read_excel('nombre_archivo.xlsx')
print(df_verificacion.head())
```

---
# 📄 Leyendo Datos desde Google Sheets

Google Sheets es una herramienta de hojas de cálculo online, parte de **Google Workspace**, que permite **crear, editar y colaborar** en hojas de cálculo en tiempo real desde la nube.

---

## 🛠️ Características de Google Sheets

* ✅ Creación y edición de hojas de cálculo.
* ➕ Funciones y fórmulas integradas.
* 📊 Gráficos, tablas dinámicas y validación de datos.
* ☁️ Acceso desde cualquier dispositivo con internet.
* 👥 **Colaboración en tiempo real**: varios usuarios pueden trabajar al mismo tiempo en el mismo documento.
* 🔄 Importación y exportación de archivos **CSV, XLSX, ODS, PDF**, entre otros.

---

## 📥 Cómo Importar un Archivo Excel (`.xlsx`) a Google Sheets

1. Accede a [Google Sheets](https://sheets.google.com) e inicia sesión con tu cuenta de Google.
2. Haz clic en **“+ Nueva hoja de cálculo”**.
3. En la hoja abierta, ve al menú **Archivo → Importar**.
4. Selecciona la pestaña **“Subir”**.
5. Sube o arrastra el archivo `.xlsx`.
6. Haz clic en **“Importar datos”**.
7. Los datos se cargarán en la hoja.

---

## 🔗 Importar desde Google Sheets a Google Colab

### 🧩 Paso a paso:

1. **Subir el archivo a Google Sheets**
   Importa tu archivo Excel (`.xlsx`) y abrelo como hoja de cálculo en Sheets.

2. **Obtener y compartir el enlace**

   * Haz clic en **"Compartir"**.
   * Elige **"Cualquiera con el enlace puede ver"**.

3. **Extraer el ID del archivo**

   * El ID está entre `/d/` y la siguiente `/` en la URL.
   * Ejemplo de URL:

     ```
     https://docs.google.com/spreadsheets/d/1A2B3C4D5E6F7G8H9I/edit#gid=0
     ```

     → ID: `1A2B3C4D5E6F7G8H9I`

4. **Guardar el ID en una variable**

```python
file_id = '1A2B3C4D5E6F7G8H9I'
```

5. **Construir la URL**

```python
sheet_name = 'nombre_de_la_hoja'  # opcional
url = f'https://docs.google.com/spreadsheets/d/{file_id}/gviz/tq?tqx=out:csv&sheet={sheet_name}'
```

* `gviz/tq` → conecta con la API de Google Sheets
* `tqx=out:csv` → especifica que el formato de salida es **CSV**
* `sheet=` → selecciona una hoja específica (si no se indica, toma la primera por defecto)

6. **Importar con Pandas**

```python
import pandas as pd

df = pd.read_csv(url)
```

7. **Verificar contenido**

```python
df.head()
```

---

## ✅ Resumen

| Elemento                    | Acción                                                         |
| --------------------------- | -------------------------------------------------------------- |
| Subir archivo               | A Google Sheets                                                |
| Compartir con enlace        | Permitir visualización pública                                 |
| Extraer ID                  | Desde la URL entre `/d/` y la siguiente `/`                    |
| Construir URL personalizada | Usando `gviz/tq`, `tqx=out:csv`, `sheet=` y f-strings          |
| Leer con Pandas             | `pd.read_csv(url)` para cargar directamente desde Google Colab |
| Hoja específica             | Añadir `sheet=nombre` en la URL para leer una hoja concreta    |

---
