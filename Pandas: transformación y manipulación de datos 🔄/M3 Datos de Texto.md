# 🐼 Módulo 3 : Datos de Texto  🔄
---

# 🧹 Manipulación de Texto en Pandas y Tokenización

## 📌 ¿Por qué es importante?

* El texto contiene **información valiosa**, como valoraciones o descripciones que pueden influir en variables como el precio.
* Procesar texto requiere **preparación previa**: limpieza, normalización y tokenización.

---

## 🧪 Manipulación de Texto en Pandas

### 🔠 Conversión a minúsculas

Para evitar inconsistencias como "Bonito" vs "bonito", se convierte el texto a minúsculas.

```python
df['descripcion'] = df['descripcion'].str.lower()
```

### 📌 `.str` y `.lower()`

| Método     | Función                                                                 |
| ---------- | ----------------------------------------------------------------------- |
| `.str`     | Accede a métodos de cadenas en columnas tipo texto (`object`) en Pandas |
| `.lower()` | Convierte todo el texto a minúsculas                                    |

---

## ✂️ Tokenización: Dividir texto en partes

### ✅ ¿Qué es tokenizar?

Es dividir un texto en **unidades más pequeñas** llamadas *tokens* (como palabras, caracteres o frases).

---

## 🧰 Pasos para Tokenizar un Texto

### 1. Obtener el texto

```python
texto = "Este es un ejemplo de texto para tokenizar."
```

---

### 2. Limpieza del texto (recomendado)

```python
import re

texto = "¡Hola! Este es un ejemplo... con símbolos."
texto = re.sub(r'[^\w\s]', '', texto)  # Quitar puntuación
texto = texto.lower()  # Minúsculas
```

🔍 Resultado: `'hola este es un ejemplo con símbolos'`

---

### 3. Tokenización por palabras

```python
tokens = texto.split()
print(tokens)
# ['hola', 'este', 'es', 'un', 'ejemplo', 'con', 'símbolos']
```

---

### 4. Normalización

#### 🔸 Stemming (Raíces de palabras)

```python
from nltk.stem import PorterStemmer
stemmer = PorterStemmer()
stemmer.stem("running")  # 'run'
```

#### 🔸 Lemmatización (Forma base)

```python
from nltk.stem import WordNetLemmatizer
lemmatizer = WordNetLemmatizer()
lemmatizer.lemmatize("better")  # 'good'
```

---

### 5. Eliminar Stop Words (palabras comunes)

```python
from nltk.corpus import stopwords
stopwords.words('spanish')  # ['de', 'la', 'que', ...]
```

---

## 🧠 Diferencia clave: `apply` vs `applymap`

| Método        | Aplica función a...            | Ideal para...            |
| ------------- | ------------------------------ | ------------------------ |
| `.apply()`    | Cada valor de una **Serie**    | Una sola columna         |
| `.applymap()` | Cada valor de un **DataFrame** | Varias columnas a la vez |

---

## 💡 Ejemplos rápidos

### ➕ `apply()` – elevar al cuadrado

```python
s = pd.Series([1, 2, 3])
s.apply(lambda x: x**2)
```

### ➕ `applymap()` – sumar 10 a cada valor

```python
df = pd.DataFrame({'A': [1, 2], 'B': [3, 4]})
df.applymap(lambda x: x + 10)
```

---
## 🧠 ¿Qué son las Expresiones Regulares (Regex)?

**Regex (Regular Expressions)** son patrones que se utilizan para buscar, extraer o reemplazar texto dentro de cadenas. Son una herramienta esencial para **limpiar, normalizar o validar** texto en tareas de análisis de datos, especialmente cuando los datos provienen de fuentes no estructuradas como formularios, correos o redes sociales.

---

## 📌 ¿Para qué sirven en ciencia de datos?

* **Limpieza de texto** (eliminación de símbolos, puntuación, etiquetas HTML, etc.)
* **Extracción de patrones** (como emails, fechas, precios, etc.)
* **Validación de formatos** (por ejemplo, verificar que una cadena sea un código postal válido)
* **Clasificación** (spam/no spam, sentimientos, categorías)

---

## 🧪 Metacaracteres comunes en Regex

| Símbolo | Significado                                                  |                   |      |
| ------- | ------------------------------------------------------------ | ----------------- | ---- |
| `.`     | Cualquier carácter (excepto salto de línea)                  |                   |      |
| `*`     | Cero o más repeticiones                                      |                   |      |
| `+`     | Una o más repeticiones                                       |                   |      |
| `?`     | Cero o una repetición                                        |                   |      |
| `[]`    | Conjunto de caracteres (ej: `[abc]`)                         |                   |      |
| `[^]`   | Negación del conjunto (ej: `[^abc]`)                         |                   |      |
| `()`    | Agrupación de patrones                                       |                   |      |
| \`      | \`                                                           | O lógico (ej: \`a | b\`) |
| `\`     | Escape de carácter especial (ej: `\.` para un punto literal) |                   |      |
| `^`     | Inicio de línea                                              |                   |      |
| `$`     | Fin de línea                                                 |                   |      |

---

## 🛠 Métodos clave en Python/Pandas para manipulación de texto

### 1. `.str.replace()` en Pandas

Permite reemplazar texto en una columna entera.

**Ejemplo básico:**

```python
df['columna'] = df['columna'].str.replace('malo', 'bueno')
```

**Ejemplo con regex:**

```python
df['columna'] = df['columna'].str.replace(r'\d+', '', regex=True)  # Elimina todos los números
```

---

### 2. `.str.strip()`

Elimina espacios en blanco al principio y al final de una cadena.

```python
texto = "  hola mundo  "
print(texto.strip())  # → "hola mundo"
```

---

## 🧹 Eliminación de guiones aislados con Regex

Cuando limpiamos texto, es útil eliminar guiones que **no están entre palabras** (por ejemplo: al final de una línea o aislados).

### 🔎 Regex usada:

```regex
(?<!\w)-(?!\w)
```

### Desglose:

* `(?<!\w)`: Negative lookbehind → **no debe haber una letra o número antes del guión**
* `-`: Coincide con el guión literal
* `(?!\w)`: Negative lookahead → **no debe haber una letra o número después del guión**

**Ejemplo en Pandas:**

```python
df['columna'] = df['columna'].str.replace(r'(?<!\w)-(?!\w)', '', regex=True).str.strip()
```

---

## 🔤 Tokenización de Texto

Es el proceso de **dividir texto en unidades (tokens)** como palabras o frases.

**Ejemplo en Python:**

```python
texto = "Hola mundo, esto es NLP"
tokens = texto.lower().split()
print(tokens)  # ['hola', 'mundo,', 'esto', 'es', 'nlp']
```

---

## 🧰 Limpieza de texto avanzada con `re` (módulo de expresiones regulares de Python)

### Ejemplo completo:

```python
import re

texto = "¡Hola! Este es un ejemplo - con símbolos y números 123."

# Eliminar caracteres especiales
texto = re.sub(r'[^\w\s]', '', texto)   # → 'Hola Este es un ejemplo  con símbolos y números 123'

# Convertir a minúsculas
texto = texto.lower()

# Eliminar números
texto = re.sub(r'\d+', '', texto)       # → 'hola este es un ejemplo  con símbolos y números '

# Eliminar espacios múltiples
texto = re.sub(r'\s+', ' ', texto).strip()

print(texto)  # → 'hola este es un ejemplo con símbolos y números'
```

---

## 🚫 Stop Words

Son palabras que aparecen frecuentemente pero no aportan valor al análisis (como “el”, “de”, “por”, “con”).

**Ejemplo con NLTK:**

```python
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize
import nltk
nltk.download('stopwords')
nltk.download('punkt')

texto = "Este es un ejemplo de texto con stop words"
palabras = word_tokenize(texto.lower())
limpio = [palabra for palabra in palabras if palabra not in stopwords.words('spanish')]

print(limpio)  # → ['ejemplo', 'texto', 'stop', 'words']
```

---

## 🧱 Conceptos clave resumidos

| Concepto             | Descripción                                          |
| -------------------- | ---------------------------------------------------- |
| **Tokenización**     | Dividir texto en unidades (palabras, frases, etc.)   |
| **Regex**            | Patrón para buscar, extraer o reemplazar texto       |
| **replace()**        | Reemplaza partes de una cadena                       |
| **strip()**          | Elimina espacios en extremos de una cadena           |
| **Guiones aislados** | Guiones sin letras alrededor (eliminables con regex) |
| **Stop words**       | Palabras vacías que no aportan valor                 |
| **Normalización**    | Unificar el texto (minúsculas, sin puntuación, etc.) |

---
