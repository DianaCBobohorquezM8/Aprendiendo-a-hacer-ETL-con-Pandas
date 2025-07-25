# 🐼 Módulo 1 : Conociendo el problema 🔄
---
# 🧠 Proyecto: Solución de Precios Inteligentes

## 🎯 **Problema de Negocio**

Crear una solución que **sugiera precios diarios óptimos** para propiedades en alquiler, tomando en cuenta:

* Comodidades
* Tamaño
* Ocupación
* Demanda temporal

> 📝 **Objetivo**: Maximizar las ganancias del anfitrión durante periodos de alta demanda.

---

## 🧹 Preparación de Datos

📌 **Importante**:
Este curso se enfoca en **preparar, transformar y manipular** los datos.
El **análisis predictivo** o el modelo de precios inteligentes **no se aborda aún**.

---

## 📂 Importación de Datos en Google Colab

### 🔼 Subida de archivos

* Google Colab **no accede directamente** a los archivos locales.
* Se debe usar el sistema de carga manual de archivos (ícono de carpeta o `files.upload()`).

### 📦 Archivo: `datos_hosting.json`

---

## 📊 Lectura de Datos con Pandas

### 1️⃣ Importar la librería Pandas

```python
import pandas as pd
```

**Función**: Herramienta esencial para la manipulación de datos.
**Alias `pd`**: Es una convención para escribir menos.

---

### 2️⃣ Leer el archivo JSON

```python
datos = pd.read_json("datos_hosting.json")
```

🔹 **`pd.read_json(path)`**:
Convierte el archivo JSON en un **DataFrame** de Pandas.

🔸 **`path`**: Ruta del archivo, puede ser local o una URL.

---

### 3️⃣ Visualización inicial

```python
print(datos.head())
```

* Muestra los primeros 5 registros.
* Se identifica que los datos están **anidados** en una columna llamada **`info-inmuebles`**.

> 🧩 Esto hace que sea necesario **normalizar o expandir** los datos para analizarlos correctamente.

---

## 📌 Ejemplo Completo

```python
import pandas as pd

# Ruta del archivo JSON
path = "datos_hosting.json"

# Leer el archivo JSON y convertirlo en DataFrame
datos = pd.read_json(path)

# Ver los primeros registros
print(datos.head())
```

---

## 📎 Conclusión

| Elemento         | Descripción                                                    |
| ---------------- | -------------------------------------------------------------- |
| `pandas`         | Biblioteca para análisis de datos en Python                    |
| `read_json()`    | Convierte datos JSON a DataFrame                               |
| `datos`          | Variable que almacena el DataFrame cargado                     |
| `datos.head()`   | Muestra los primeros registros del DataFrame                   |
| `info-inmuebles` | Columna con **datos anidados**, requiere tratamiento posterior |

---
# 💸 **Pricing Inteligente para Alojamiento**

## 🧠 ¿Qué es?

El **pricing inteligente** es una **estrategia automatizada y dinámica** para estimar precios de alojamiento en función de múltiples factores. Su objetivo es **maximizar ingresos** y **rentabilidad** para los propietarios.

---

## 🔍 Factores que considera

* 📈 Oferta y demanda
* 🗓️ Estacionalidad (temporadas altas y bajas)
* 🎉 Eventos locales (conciertos, ferias, festivales)
* 📍 Ubicación y características del alojamiento
* 🛏️ Comodidades, tamaño, ocupación, etc.

---

## ⚙️ ¿Cómo funciona?

Un **algoritmo de precios inteligentes** ajusta automáticamente las tarifas diarias:

| Situación                              | Acción del algoritmo                     |
| -------------------------------------- | ---------------------------------------- |
| 📊 Aumento de la demanda               | Incrementa el precio                     |
| 📉 Disminución de la demanda           | Reduce el precio para mantener ocupación |
| 📆 Eventos locales o fechas especiales | Ajusta precios al alza                   |
| 🔒 Temporadas de baja ocupación        | Ofrece precios más competitivos          |

---

## 🧩 Tecnologías utilizadas

### 🤖 Aprendizaje Automático (Machine Learning)

* Analiza grandes volúmenes de datos históricos.
* Detecta **patrones de comportamiento del consumidor**.
* Ajusta los precios de forma más **precisa** y **predictiva**.

### 🧠 Reglas y Heurísticas (Alternativas)

* Sistema basado en **lógica predefinida**.
* Define condiciones como:

  * "Si la ocupación < 50%, bajar precio un 10%"
  * "Si es fin de semana, aumentar precio 15%"

> ⚠️ Aunque es más simple, este enfoque es **menos flexible** y menos eficiente con grandes volúmenes de datos o escenarios complejos.

---

## 🏆 Ventajas del Pricing Inteligente

✅ Maximiza ingresos en momentos de alta demanda  
✅ Mantiene la ocupación en temporada baja  
✅ Aumenta la competitividad frente a otras propiedades  
✅ Se adapta automáticamente a condiciones del mercado  

---
# 🧩 Comprendiendo los Datos JSON y Preparación para Análisis

## 📦 ¿Qué es `json_normalize()`?

### 🔧 Función:

`pandas.json_normalize()` es una función de Pandas utilizada para **convertir estructuras de datos JSON anidadas** (como diccionarios o listas dentro de listas) en un **DataFrame plano**, es decir, en **una tabla con columnas y filas** fácilmente analizable.

### 🔍 ¿Por qué usarla?

* JSON es un formato flexible y común en APIs y bases de datos web.
* Muchos archivos JSON tienen **datos anidados**, lo que dificulta el análisis directo.
* Esta función **extrae las claves de diccionarios** y las convierte en **columnas**.

### 📌 Ejemplo:

```python
from pandas import json_normalize

# Suponiendo que ya leíste el JSON en una variable llamada datos
df = json_normalize(datos['info_inmuebles'])  # Accede al diccionario anidado
```

---

## 🧱 Extracción de Diccionarios como Columnas

### 🧩 ¿Qué significa?

Si tienes una columna (por ejemplo, `info_inmuebles`) donde cada celda contiene un **diccionario** como:

```json
{"habitaciones": 3, "baños": 2}
```

Al extraerlo, tendrás columnas separadas:

| habitaciones | baños |
| ------------ | ----- |
| 3            | 2     |

### ✅ ¿Por qué es útil?

* 📊 Facilita el análisis y la visualización.
* 🧮 Permite aplicar funciones estadísticas directamente sobre las columnas.
* 🔎 Hace más sencillo filtrar, agrupar y graficar.

---

## 🔍 Exploración de Tipos de Variables

### 📘 ¿Qué es?

Implica identificar qué tipo de datos contiene cada columna después de la normalización:

| Tipo de Dato | Ejemplo                          |
| ------------ | -------------------------------- |
| Numérico     | `habitaciones = 3`               |
| Texto        | `descripción = "Cómodo estudio"` |
| Lista        | `comodidades = ["WiFi", "TV"]`   |
| Booleano     | `tiene_parqueadero = True`       |

### 🎯 ¿Por qué es importante?

* 🧠 Cada tipo de dato tiene **distintas funciones y tratamientos**.
* 🛠️ Evita errores en cálculos, gráficos o modelos.
* 🧪 Permite elegir la mejor técnica para limpieza y transformación.

---

## 🖼️ Visualización de los Datos

### 🔍 ¿Qué significa?

Representar los datos de forma gráfica o tabular para **detectar patrones y errores** más fácilmente.

### 💡 ¿Por qué es útil?

* Permite ver **tendencias**.
* Facilita la **detección de valores atípicos**.
* Mejora la **comprensión de la distribución** de los datos.
---

