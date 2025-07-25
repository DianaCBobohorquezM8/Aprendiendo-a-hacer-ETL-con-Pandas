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

