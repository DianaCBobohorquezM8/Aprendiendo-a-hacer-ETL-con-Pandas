# 🐼 Módulo 2 : Datos numéricos  🔄
---
# 🧬 Transformación de Listas en el DataFrame con `explode()`

## 📌 ¿Por qué transformar listas en filas?

Cuando trabajamos con **datos reales**, es común encontrar columnas donde las celdas contienen **listas de elementos**. Por ejemplo, una propiedad puede tener múltiples **comodidades** como `["WiFi", "TV", "Piscina"]`, todas en una sola celda. Para **analizar individualmente cada comodidad**, necesitamos **separarlas en filas**.

---

## 🔧 Método: `.explode()`

### 🔍 ¿Qué hace?

Convierte cada elemento de una lista contenida en una celda en **una nueva fila** del DataFrame, **repitiendo el resto de los valores de la fila original**.

### 🧠 ¿Por qué es útil?

* Facilita análisis como: cuántas propiedades tienen cierta comodidad.
* Permite visualizar la frecuencia de elementos individuales.
* Prepara los datos para **agrupamientos y filtros más detallados**.

### 🧪 Ejemplo:

```python
# Explota la columna 'comodidades' que contiene listas
datos = datos.explode('comodidades')
```

---

## 🔄 Resetear el índice con `.reset_index()`

Después de usar `.explode()`, el índice del DataFrame puede quedar **desordenado** o duplicado.

### ✔ Solución:

```python
datos.reset_index(inplace=True, drop=True)
```

* `inplace=True`: modifica el DataFrame original.
* `drop=True`: elimina el índice anterior (evita que se cree una columna con los índices viejos).

---

## 🧾 Inspección de tipos con `.info()`

Para asegurarte de que los datos están limpios y listos para análisis, es fundamental revisar los **tipos de cada columna**:

```python
datos.info()
```

Este comando devuelve:

* Nombres de columnas.
* Tipo de dato (`int64`, `float64`, `object`, etc.).
* Cantidad de valores no nulos.

---

## 🗃️ Descripción de las columnas en `datos_hosting.json`

| Columna                | Descripción                              |
| ---------------------- | ---------------------------------------- |
| `evaluacion_general`   | Puntuación media del alojamiento.        |
| `experiencia_local`    | Actividades ofrecidas en la estancia.    |
| `max_hospedes`         | Número máximo de huéspedes permitidos.   |
| `descripcion_local`    | Descripción de la propiedad.             |
| `descripcion_vecindad` | Descripción del vecindario.              |
| `cantidad_baños`       | Número total de baños.                   |
| `cantidad_cuartos`     | Número de habitaciones disponibles.      |
| `cantidad_camas`       | Número de camas en la propiedad.         |
| `modelo_cama`          | Tipo o modelo de cama ofrecida.          |
| `comodidades`          | Lista de comodidades (WiFi, TV, etc.).   |
| `cuota_deposito`       | Tarifa mínima de depósito por seguridad. |
| `cuota_limpieza`       | Tarifa cobrada por limpieza.             |
| `precio`               | Precio base diario por la estancia.      |

---

## 💡 Puntos clave del proceso

| Paso                         | Descripción                                                 |
| ---------------------------- | ----------------------------------------------------------- |
| Detectar columnas con listas | Usualmente tipo `object` que contienen listas en cada fila. |
| Aplicar `.explode()`         | Convierte cada elemento de la lista en una fila nueva.      |
| Usar `.reset_index()`        | Reorganiza los índices para evitar errores posteriores.     |
| Revisar `.info()`            | Verifica estructura y tipos de datos del DataFrame.         |

---

## 🧭 Ejemplo completo

```python
# Explota la columna de listas
datos = datos.explode('comodidades')

# Resetea el índice para reorganizar el DataFrame
datos.reset_index(inplace=True, drop=True)

# Inspecciona la estructura del DataFrame
datos.info()
```

---
# 🔁 Transformar Datos Textuales en Datos Numéricos con `astype()`

## 🎯 ¿Por qué convertir datos?

Los modelos de análisis y las visualizaciones necesitan **datos numéricos**. Si tienes datos en formato de texto como `"5"` o `"250.00"`, primero necesitas convertirlos al tipo adecuado (entero o decimal) para poder operar con ellos.

---

## 🔢 Tipos de datos numéricos más comunes

| Tipo de Dato | Descripción                        | Numpy        |
| ------------ | ---------------------------------- | ------------ |
| `int64`      | Entero de 64 bits (sin decimales)  | `np.int64`   |
| `float64`    | Decimal de 64 bits (con decimales) | `np.float64` |

> ℹ️ **Numpy (`np`)** es una biblioteca que facilita el trabajo con datos numéricos en Python.

---

## 📦 Importar Numpy

```python
import numpy as np
```

---

## 🔧 Conversión con `astype()`

### 🧠 ¿Qué es `astype()`?

Es un método de Pandas que permite **cambiar el tipo de dato** de una columna en un DataFrame.

### 🧪 Sintaxis

```python
df['columna'] = df['columna'].astype(np.tipo_de_dato)
```

---

## 📍 Ejemplos prácticos

### ✅ Convertir una columna a entero (`int64`)

```python
datos['Max_Hospedes'] = datos['Max_Hospedes'].astype(np.int64)
```

### ✅ Convertir una columna a decimal (`float64`)

```python
datos['evaluacion_general'] = datos['evaluacion_general'].astype(np.float64)
```

---

### 🔁 Convertir varias columnas a entero

```python
columnas_numericas = ['cantidad_baños', 'cantidad_cuartos', 'cantidad_camas']
for columna in columnas_numericas:
    datos[columna] = datos[columna].astype(np.int64)
```

---

## ⚠️ Problemas comunes: caracteres no numéricos

Si una columna contiene caracteres como `$`, `%` o comas (`,`), **no se puede convertir directamente**. Es necesario limpiarla antes.

### 🧹 Ejemplo de limpieza previa

```python
datos['precio'] = datos['precio'].str.replace('$', '').str.replace(',', '')
datos['precio'] = datos['precio'].astype(np.float64)
```

> ✅ Usa `.str.replace()` para eliminar caracteres no deseados **antes** de aplicar `astype()`.

---

## 📌 Resumen Visual de Uso

| Acción                           | Código                                                |
| -------------------------------- | ----------------------------------------------------- |
| Convertir a entero               | `df['col'] = df['col'].astype(np.int64)`              |
| Convertir a decimal              | `df['col'] = df['col'].astype(np.float64)`            |
| Convertir múltiples columnas     | `for col in cols: df[col] = df[col].astype(np.int64)` |
| Limpiar texto antes de convertir | `df['col'] = df['col'].str.replace(...).astype(...)`  |

---
# 🎯 Valores Numéricos en Python (Pandas + Numpy)

## 🧠 ¿Por qué importa la precisión?

Cuando se trabaja con grandes volúmenes de datos o recursos limitados de memoria, es importante encontrar un equilibrio entre:

* **Precisión** (qué tan exactos son los datos).
* **Uso de memoria** (qué tanto espacio ocupan).

---

## 🧮 Conceptos clave

| Término       | Definición                                                                                                             |
| ------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **Bit**       | Unidad mínima de información (0 o 1).                                                                                  |
| **Byte**      | Grupo de 8 bits.                                                                                                       |
| **Precisión** | Número de bits utilizados para representar un valor. A mayor precisión, mayor rango de valores y mayor uso de memoria. |

---

## 🔢 Tipos de datos **enteros** en Numpy

Los enteros pueden ocupar diferentes cantidades de **bits**, lo que afecta el **rango** de valores representables.

| Tipo    | Bits | Rango Mínimo               | Rango Máximo              |
| ------- | ---- | -------------------------- | ------------------------- |
| `int8`  | 8    | -128                       | 127                       |
| `int16` | 16   | -32.768                    | 32.767                    |
| `int32` | 32   | -2.147.483.648             | 2.147.483.647             |
| `int64` | 64   | -9.223.372.036.854.775.808 | 9.223.372.036.854.775.807 |

✅ **`int64`**: común por defecto en Pandas.   
💡 Usa **`int32`, `int16`, o `int8`** si sabes que los valores serán pequeños → **ahorras memoria**.

---

## 🌊 Tipos de datos **decimales** (float)

Los números de **punto flotante** también tienen distintas precisiones:

| Tipo      | Bits | Precisión decimal aproximada |
| --------- | ---- | ---------------------------- |
| `float32` | 32   | \~7 dígitos decimales        |
| `float64` | 64   | \~15 dígitos decimales       |

✅ **`float64`**: recomendado para datos científicos y financieros.   
✅ **`float32`**: útil cuando se necesita reducir uso de memoria (por ejemplo, en modelos de machine learning).

---

## 🧪 Ejemplos de conversión en Pandas

```python
import numpy as np

# Convertir columna a int32
datos['edad'] = datos['edad'].astype(np.int32)

# Convertir columna a float32
datos['precio'] = datos['precio'].astype(np.float32)
```

---

## 📌 ¿Qué tipo elegir?

| Situación                       | Tipo recomendado   | Razón                                   |
| ------------------------------- | ------------------ | --------------------------------------- |
| Datos pequeños                  | `int8`, `int16`    | Ahorro de memoria                       |
| Rango moderado de enteros       | `int32`            | Buen equilibrio entre rango y memoria   |
| Datos científicos o financieros | `int64`, `float64` | Máxima precisión necesaria              |
| Modelos de Machine Learning     | `float32`          | Menor carga de memoria sin perder mucho |

---

## 💡 Buenas prácticas

* Siempre **verifica el rango** de tus datos antes de convertir el tipo.
* Ahorra memoria cuando sea posible, **sin comprometer precisión**.
* Utiliza `astype()` para conversiones específicas y controladas.

---
# 🧹 Limpieza de Datos Numéricos en Texto usando `apply()`

Cuando los valores numéricos vienen como texto (`str`), debemos limpiarlos para convertirlos en números válidos (`float`). Esto es común con datos como precios o cantidades que tienen símbolos, comas o espacios.

---

## 🚩 Problema

**Los valores numéricos están mal formateados:**

Ejemplos comunes:

```plaintext
"$1,200.00"
" 3,450 "
"USD 500.75"
```

Python no puede interpretarlos como `float` sin limpiar primero los caracteres no deseados.

---

## 🎯 Objetivo

Convertir strings como `"$1,200.00"` en valores numéricos `float`, como `1200.00`.

---

## 🧰 Herramientas utilizadas

| Método      | Descripción                                        |
| ----------- | -------------------------------------------------- |
| `apply()`   | Aplica una función a cada elemento de una columna. |
| `lambda`    | Función anónima en línea.                          |
| `replace()` | Reemplaza texto dentro de strings.                 |
| `strip()`   | Elimina espacios en blanco alrededor del texto.    |

---

## 🧪 Ejemplo práctico

```python
import pandas as pd

# Supongamos que tenemos un DataFrame con precios en texto
df = pd.DataFrame({'precio': ['$1,200.00', ' $3,450.50 ', '$500.75']})

# Limpieza del texto y conversión a float
df['precio'] = df['precio'].apply(lambda x: x.replace('$', '').replace(',', '').strip())
df['precio'] = df['precio'].astype(float)

print(df)
```

### 🔍 ¿Qué hace cada parte?

```python
lambda x: x.replace('$', '').replace(',', '').strip()
```

| Operación         | Función usada       | Resultado                           |
| ----------------- | ------------------- | ----------------------------------- |
| Eliminar símbolo  | `.replace('$', '')` | "\$1,200.00" → "1,200.00"           |
| Eliminar comas    | `.replace(',', '')` | "1,200.00" → "1200.00"              |
| Eliminar espacios | `.strip()`          | " 1200.00 " → "1200.00"             |
| Convertir a float | `.astype(float)`    | "1200.00" (str) → 1200.00 (`float`) |

---

## ✅ Resultado final

```plaintext
   precio
0  1200.00
1  3450.50
2   500.75
```

---

## 📌 Recomendaciones

* Verifica siempre que los datos limpios puedan convertirse a `float`.
* Si tienes símbolos diferentes (€, %, etc.), agrégalos también en `.replace()`.
* Si los datos están en otras columnas, aplica la misma lógica cambiando el nombre de la columna.

---
