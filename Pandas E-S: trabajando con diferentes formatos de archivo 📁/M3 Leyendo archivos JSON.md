# 🐼 Módulo  3 : Leyendo archivos JSON  📁
---
# 📁 Importando Archivos JSON con Pandas

Un archivo **JSON** (*JavaScript Object Notation*) es un **formato de texto ligero** para almacenar e intercambiar datos. Es fácil de leer para humanos y fácil de procesar por las máquinas.

---

## 🧠 ¿Para Qué Sirve JSON?

* ✅ Ligero y eficiente para la transmisión de datos.
* 🔗 Compatible con la mayoría de lenguajes de programación.
* 📦 Muy utilizado en **APIs** para intercambiar datos entre aplicaciones web, móviles y servidores.

---

## 🔄 Cómo Funciona el Intercambio con JSON (vía API)

1. **Solicitud (Request):** Una aplicación cliente solicita datos al servidor vía API.
2. **Procesamiento:** El servidor realiza operaciones (consultas, cálculos, etc.).
3. **Respuesta en JSON:** El servidor responde con los datos estructurados en **clave-valor**.
4. **Recepción y deserialización:** El cliente convierte el JSON en un objeto manejable (por ejemplo, un DataFrame).

> 📖 **Analogía:**
> Tú (cliente) pides un plato en un restaurante (servidor). El camarero (API) te lo trae servido en una bandeja clara (JSON). Tú lo consumes (deserializas y usas).

---

## 🔍 Estructura Básica de un JSON

```json
{
  "nombre": "Ana",
  "edad": 28,
  "ciudad": "Bogotá"
}
```

* **Llaves (keys):** nombre, edad, ciudad
* **Valores (values):** "Ana", 28, "Bogotá"

---

## 🛠️ Lectura de JSON con Pandas

### ✅ Pasos para leer un JSON

```python
# Paso 1: Importar Pandas
import pandas as pd

# Paso 2: Leer el archivo JSON
df = pd.read_json('archivo.json')

# Paso 3: Verificar el contenido
df.head()
```

---

## 📌 Conceptos Relacionados

| Concepto                | Descripción                                                                         |
| ----------------------- | ----------------------------------------------------------------------------------- |
| **read\_json()**        | Método de Pandas para leer archivos JSON.                                           |
| **Llave-valor**         | Estructura interna del JSON, se convierte en columnas y valores en el DataFrame.    |
| **Información anidada** | Diccionarios dentro de diccionarios. Requiere tratamiento adicional para desanidar. |
| **APIs**                | Interfaces que permiten la comunicación entre sistemas usando JSON.                 |
| **Visualizadores JSON** | Herramientas online que permiten ver estructuras complejas de forma legible.        |

---

## 🔄 Manejo de Información Anidada

```json
{
  "paciente": {
    "nombre": "Luis",
    "edad": 35
  },
  "diagnostico": "Gripe"
}
```

* Este tipo de estructura requiere:

  * Acceso con `json_normalize()`
  * Tratamiento adicional con `.apply()` o listas por comprensión.

```python
import json
from pandas import json_normalize

with open('archivo.json') as f:
    data = json.load(f)

df = json_normalize(data)
```

---

## ✅ Resumen

| Elemento         | Detalle                                                                 |
| ---------------- | ----------------------------------------------------------------------- |
| Formato JSON     | Texto estructurado, clave-valor                                         |
| Uso              | Transmisión de datos entre aplicaciones, común en APIs                  |
| Método en Pandas | `read_json()`                                                           |
| Requiere Pandas  | `import pandas as pd`                                                   |
| Desafío          | Leer información anidada → `json_normalize()` o procesamiento adicional |

---
# 🧩 Manejo y Normalización de Archivos JSON Anidados con Pandas

Cuando trabajamos con archivos JSON que contienen **estructura anidada** (listas o diccionarios dentro de diccionarios), es necesario **transformar esos datos** para analizarlos de forma tabular en Pandas. Aquí entra en juego `json_normalize()`.

---

## 🧱 ¿Qué es un JSON?

* **JSON (JavaScript Object Notation)** es un formato de texto usado para representar datos estructurados.
* Es comúnmente utilizado para transmitir datos entre un servidor y una aplicación web mediante **APIs**.
* Se organiza en pares **llave\:valor**, y puede tener valores anidados (listas o diccionarios dentro de diccionarios).

---

## 🛠️ Lectura de JSON anidado con Pandas

```python
import pandas as pd
import json

# Abrir el archivo JSON
with open('Pacientes2.json') as archivo:
    datos_pacientes_2 = json.load(archivo)
```

---

## 🔍 Estructura del JSON

Para entender mejor el archivo, se utilizó el visualizador [**JSON Crack**](https://jsoncrack.com/), donde se identificó:

* El archivo contiene una clave principal `"pacientes"`, que guarda **una lista de diccionarios** (cada uno representa un paciente).
* Dentro de cada diccionario (paciente), existe una clave `"problemas de salud"` que almacena **otro diccionario anidado** con más detalles.

---

## 🧪 Proceso de Normalización

La estructura anidada **no se puede analizar directamente** con `read_json()`. Por eso se usó `pandas.json_normalize()`:

```python
from pandas import json_normalize

df_normalizado = json_normalize(datos_pacientes_2, record_path=['pacientes'])
```

Este método:

* Toma la **clave `'pacientes'` como el nivel que se desea descomponer**.
* Crea columnas nuevas con los subcampos de cada paciente, incluyendo los que estaban en `"problemas de salud"`.

---

## ✅ Resultado

* El DataFrame resultante `df_normalizado` contiene **columnas planas** (no anidadas).
* Todos los campos dentro de `"problemas de salud"` ahora son **columnas independientes**.
* Esto facilita:

  * 🔍 Inspección de datos.
  * 📈 Análisis estadístico.
  * 📤 Exportación a CSV/Excel.

---

## 🧠 ¿Por qué usar `json_normalize()`?

| Ventaja           | Descripción                                              |
| ----------------- | -------------------------------------------------------- |
| 📦 Organización   | Convierte estructuras complejas en tablas comprensibles. |
| 🧩 Desanidamiento | Extrae claves internas como columnas.                    |
| 💻 Análisis       | Permite usar `groupby`, `filter`, visualización, etc.    |

---

## 📝 Resumen visual del flujo

```plaintext
📁 Pacientes2.json (estructura anidada)
       ↓
🔎 Visualizado con JSON Crack
       ↓
🧪 Normalización con json_normalize()
       ↓
📊 df_normalizado (estructura tabular, columnas planas)
```

---
