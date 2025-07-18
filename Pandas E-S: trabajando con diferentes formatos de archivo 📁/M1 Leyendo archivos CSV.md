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
¡Exacto! Aquí tienes ese concepto organizado en un formato claro y breve en **Markdown**, ideal para complementar tus apuntes:

---

## ⚠️ Importancia del Parámetro `sep` en `pd.read_csv()`

Cuando lees un archivo CSV con **Pandas**, es fundamental indicar el **separador correcto de los campos** usando el parámetro `sep`.

### 🔹 Valor predeterminado:
Cuando usamos pd.read_csv(), Pandas asume por defecto que el separador es una coma (,).  
Si tu archivo utiliza otro carácter—por ejemplo, punto y coma (;)—es esencial especificarlo con el parámetro sep. 
De lo contrario, los datos podrían cargarse incorrectamente.


```python
pd.read_csv('archivo.csv')
```

> Asume que los campos están separados por comas `,`.

---

### 🛑 Problema común

Si el archivo utiliza **otro separador** (por ejemplo, punto y coma `;`), el DataFrame puede quedar con una sola columna mal estructurada.

---

### ✅ Solución: Usar `sep=';'`

```python
import pandas as pd

# Leer un archivo CSV con punto y coma como separador
df = pd.read_csv('archivo.csv', sep=';')
```
•	Aquí indicamos sep=';' para que Pandas divida las columnas correctamente.  
•	Si no se especifica, todo se cargaría en una sola columna, con los valores como texto con ; incluido.

  🧠 Resumen
  
    •	🗂️ sep=',' (por defecto): Archivos separados por comas.     
    •	🗂️ sep=';' o sep='\t': Ideal para CSV con otros separadores.


### 📌 Tip: ¿No sabes qué separador usa tu archivo?

Abre el archivo `.csv` con un editor de texto o Excel y revisa si los campos están separados por:

* `,` → coma
* `;` → punto y coma
* `\t` → tabulación

Luego ajusta el valor de `sep` según corresponda.

---
# 💾 Escribir Archivos CSV con `to_csv()` en Pandas

El método `to_csv()` te permite **guardar un DataFrame como un archivo CSV**, ideal para compartir, respaldar o analizar los datos en otras plataformas.

---

## 🧩 Sintaxis Básica

```python
nombre_del_dataframe.to_csv('nombre_del_archivo.csv', opciones)
```

### Parámetros:

* `nombre_del_dataframe`: el DataFrame que quieres exportar.
* `'nombre_del_archivo.csv'`: nombre del archivo de salida (con extensión `.csv`).
* `opciones`: parámetros opcionales para personalizar la exportación.

---

## 🔹 ¿Qué es el índice (`index`)?

El **índice** es una etiqueta que identifica las filas del DataFrame.
Por defecto, Pandas lo incluye como una **columna adicional** al exportar a CSV.

### 🚫 ¿Por qué a veces no quieres incluir el índice?

* Generalmente no es parte de los datos reales.
* Puede generar confusión si solo es un número secuencial (0, 1, 2...).
* No es necesario si ya tienes una columna que identifica las filas (como un ID de cliente).

---

## ✅ Cómo evitar que el índice se guarde

Usa `index=False` dentro de `to_csv()`:

```python
df.to_csv('nombre_del_archivo.csv', index=False)
```

---

## 🧪 Ejemplo Completo

```python
import pandas as pd

# Crear un DataFrame
data = {
    'nombre': ['Alice', 'Bob', 'Charlie'],
    'edad': [25, 30, 28],
    'ciudad': ['Nueva York', 'Londres', 'París']
}
df = pd.DataFrame(data)

# Exportar sin índice
df.to_csv('clientes.csv', index=False)
```

### 🔎 Resultado en el archivo `clientes.csv`:

```
nombre,edad,ciudad
Alice,25,Nueva York
Bob,30,Londres
Charlie,28,París
```

---

## 📌 Recomendación

🔍 Explora la [documentación oficial de `to_csv()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_csv.html) para conocer más opciones útiles, como:

* `sep=';'` → usar punto y coma como separador
* `columns=[...]` → exportar solo columnas seleccionadas
* `encoding='utf-8'` → codificación del archivo

---
# 📚 Lectura avanzada de archivos CSV con `read_csv()` 

Cuando los archivos CSV no siguen un formato estándar (como separadores diferentes, encabezados extra o líneas innecesarias), puedes personalizar la lectura con varios parámetros de `read_csv()`.

---

## 🧩 Parámetros útiles

### 🔸 `encoding='ISO-8859-1'`

* Define la **codificación de caracteres** del archivo.
* **`ISO-8859-1`** es común en archivos en idiomas latinos como portugués y español.

```python
df = pd.read_csv('archivo.csv', encoding='ISO-8859-1')
```

---

### 🔸 `sep=';'`

* Especifica el **separador de campos**.
* En muchos países europeos, el **punto y coma (;)** se usa en lugar de la coma.

```python
df = pd.read_csv('archivo.csv', sep=';')
```

---

### 🔸 `skiprows=3`

* **Ignora las primeras 3 líneas** del archivo al leerlo.
* Útil si el archivo tiene encabezados o notas previas que no forman parte de los datos.

```python
df = pd.read_csv('archivo.csv', skiprows=3)
```

---

### 🔸 `skipfooter=9`

* **Ignora las últimas 9 líneas** del archivo, típicamente usadas para totales o notas al pie.
* Requiere usar el parámetro `engine='python'`.

```python
df = pd.read_csv('archivo.csv', skipfooter=9, engine='python')
```

---

### 🔸 `engine='python'`

* Indica que el **motor de lectura** será Python (en vez del predeterminado ‘C’).
* Necesario cuando usas opciones como `skipfooter`.

---

## 🧪 Ejemplo completo

```python
import pandas as pd

df = pd.read_csv(
    'clientes.csv',
    sep=';',
    encoding='ISO-8859-1',
    skiprows=3,
    skipfooter=9,
    engine='python'
)
```

---


