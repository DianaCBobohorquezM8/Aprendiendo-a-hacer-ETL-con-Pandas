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

## 🛠️ Lectura de JSON

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

## 🛠️ Lectura de JSON anidado

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
# 🧾 Resumen: Normalización de JSON con `json_normalize()`

## 📌 ¿Qué es?

La función `pd.json_normalize()` convierte estructuras JSON (diccionarios o listas anidadas) en DataFrames, lo que facilita su análisis en ciencia de datos.

---

## 🔹 Casos Comunes

### 1. JSON Simple

```python
datos = {'Análisis': 'Indicadores', 'Año': 2020, 'Pacientes': 3}
pd.json_normalize(datos)
````

🔸 Crea una fila con columnas según las llaves del diccionario.

---

### 2. Lista de Diccionarios

```python
json_lista = [{'ID': '01', 'Edad': '55-59'}, {'ID': '02', 'Edad': '80 ó +'}]
pd.json_normalize(json_lista)
```

🔸 Cada objeto se convierte en una fila.

---

### 3. Diccionario con Subdiccionario

```python
json_obj = {'ID': '01', 'Salud': {'IMC': 16.6, 'Cardiaca': 'No'}}
pd.json_normalize(json_obj)
```

🔸 Columnas con prefijo: `Salud.IMC`, `Salud.Cardiaca`.

---

### 4. Lista de Diccionarios con Subdiccionarios

```python
json_list = [
  {'ID': '01', 'Salud': {'IMC': 16.6}},
  {'ID': '02', 'Salud': {'IMC': 20.3}}
]
pd.json_normalize(json_list)
```

🔸 Cada registro se expande en columnas tabulares.

---

### 5. JSON con Lista Anidada (y meta)

```python
pd.json_normalize(
  datos_dict,
  record_path=['Pacientes'],
  meta=['Investigación', 'Año']
)
```

🔸 `record_path`: define la lista que se expandirá.
🔸 `meta`: añade columnas externas como "Año" o "Investigación".

---

## 📁 Lectura desde archivo `.json`

```python
import json
with open('archivo.json', 'r') as f:
    datos = json.loads(f.read())

pd.json_normalize(datos, record_path='Pacientes', meta=['Investigación', 'Año'])
```

---

## ✅ Conclusión

* `json_normalize()` permite trabajar con JSON estructurados de forma eficiente.
* Usa `record_path` y `meta` para controlar qué se convierte en columnas.
* Ideal para convertir datos de APIs, encuestas o registros médicos a DataFrame.

---

## 🔗 Recurso útil

* [📚 Pandas `json_normalize()` Docs](https://pandas.pydata.org/docs/reference/api/pandas.json_normalize.html)
---
# 📝 Escribiendo Archivos JSON

## 📤 1. Exportar a JSON

Usa el método `to_json()` para exportar un DataFrame a formato JSON.

```python
df.to_json("nombre_archivo.json")
````

---

## 🗂️ 2. Nombre del Archivo

* Asegúrate de incluir la extensión `.json` al definir el nombre del archivo de salida.

---

## ✅ 3. Verificación

Para comprobar que el archivo se guardó correctamente, usa `read_json()`:

```python
pd.read_json("nombre_archivo.json")
```

---

## 📌 4. Índice

* A diferencia de `to_csv()`, **no necesitas** usar `index=False` al exportar a JSON.
* Pandas maneja el índice automáticamente en este formato.

---
# 🍎 Acceso a APIs y Datos JSON: Caso Fruitvice

## 🔍 ¿Qué es una API?

- Una **API (Application Programming Interface)** es una interfaz que permite la comunicación entre aplicaciones o sistemas.
- Las APIs permiten **obtener datos externos** de forma estructurada.
- Uno de los formatos más comunes en las APIs es **JSON** (JavaScript Object Notation), un formato ligero, basado en texto, ideal para intercambiar datos.

---

## 📘 Caso Práctico: Empresa de Alimentos Saludables

**Problema**:  
Una empresa tiene baja aceptación de sus productos por la falta de información nutricional en sus etiquetas.

**Solución propuesta**:
- Acceder a la **API de Fruitvice** para obtener los **valores nutricionales de las frutas**.
- Usar esta información para mejorar etiquetas, marketing y desarrollo de nuevos productos.

---

## 🛠️ Accediendo a la API Fruitvice con Python

### 1. Importar bibliotecas necesarias

```python
import requests
import json
import pandas as pd
````

---

### 2. Hacer la solicitud a la API

```python
datos_frutas = requests.get('https://fruityvice.com/api/fruit/all')
```

📌 Usamos `requests.get(url)` para hacer la petición.

---

### 3. Procesar la respuesta en JSON

```python
resultado = json.loads(datos_frutas.text)
```

* `datos_frutas.text`: devuelve la respuesta en texto.
* `json.loads()`: convierte el texto en una estructura Python (lista de diccionarios).

---

### 4. Visualizar los datos como DataFrame

```python
df_frutas = pd.DataFrame(resultado)
df_frutas.head()
```

📊 Ejemplo de salida:

| genus  | name    | id | family    | order    | nutritions                                                               |
| ------ | ------- | -- | --------- | -------- | ------------------------------------------------------------------------ |
| Malus  | Apple   | 6  | Rosaceae  | Rosales  | {'carbohydrates': 11.4, 'protein': 0.3, 'fat': 0.4, 'calories': 52, ...} |
| Prunus | Apricot | 35 | Rosaceae  | Rosales  | {'carbohydrates': 3.9, 'protein': 0.5, ...}                              |
| Persea | Avocado | 84 | Lauraceae | Laurales | {'carbohydrates': 8.53, 'protein': 2, ...}                               |

---

## 📌 Conceptos Clave

* **API**: puerta de acceso a datos o servicios externos.
* **JSON**: formato estructurado y ligero para compartir datos.
* **`requests.get()`**: realiza solicitudes HTTP.
* **`json.loads()`**: convierte texto JSON a objetos de Python.
* **`pd.DataFrame()`**: transforma listas/diccionarios en tablas legibles.

---

## ✅ Beneficios para la Empresa

* Añadir **información nutricional confiable** a etiquetas.
* Crear productos según necesidades nutricionales reales.
* Generar **confianza** en consumidores preocupados por su salud.

---

## 🔗 Recursos

* [🌐 Fruitvice API](https://www.fruityvice.com)
* [📚 Documentación de `requests`](https://docs.python-requests.org)
* [📘 JSON Viewer Online](https://jsoncrack.com/)
---
