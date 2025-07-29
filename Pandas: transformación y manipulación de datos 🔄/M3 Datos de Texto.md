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
### 🧪 Metacaracteres comunes en Regex

| Símbolo | Significado                                                                 |
|---------|------------------------------------------------------------------------------|
| `.`     | Cualquier carácter (excepto salto de línea)                                 |
| `*`     | Cero o más repeticiones del carácter o grupo anterior                       |
| `+`     | Una o más repeticiones del carácter o grupo anterior                        |
| `?`     | Cero o una repetición del carácter o grupo anterior                         |
| `[]`    | Conjunto de caracteres (ej: `[abc]` busca "a", "b" o "c")                   |
| `[^]`   | Negación del conjunto (ej: `[^abc]` busca cualquier carácter excepto "a,b,c")|
| `()`    | Agrupación de patrones (para capturar o aplicar operadores)                 |
| `\|`    | O lógico (ej: `a\|b` coincide con "a" o "b")                                 |
| `\`     | Escape de carácter especial (ej: `\.` busca un punto literal)               |
| `^`     | Inicio de línea                                                              |
| `$`     | Fin de línea                                                                 |


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
### 🧹 **Limpieza de texto con expresiones regulares en Pandas**

#### 🛠️ **¿Qué hicimos?**

Se aplicaron expresiones regulares (regex) sobre la columna `descripción_local` para limpiar el texto:

#### 1️⃣ **Eliminar caracteres especiales (excepto letras, números, guiones y comillas simples)**

```python
datos['descripción_local'] = datos['descripción_local'].str.replace('[^a-zA-Z0-9\-\' ]', ' ', regex=True)
```

##### ✔️ ¿Qué hace esta expresión?

* Reemplaza cualquier carácter que **no** sea:

  * Letras minúsculas (`a-z`)
  * Letras mayúsculas (`A-Z`)
  * Números (`0-9`)
  * Guiones (`-`)
  * Comillas simples (`'`)
  * Espacios (` `)
* Los caracteres encontrados se reemplazan por un espacio.

##### 🔍 Explicación de la regex:

* `[^...]`: busca todo lo que **no** esté dentro del conjunto.
* `a-zA-Z0-9\-\'`: los caracteres permitidos (notar el uso de `\` para escapar `-` y `'`).
* `regex=True`: indica que `pat` es una expresión regular.

---

#### 2️⃣ **Eliminar guiones que estén aislados (no rodeados por letras o números)**

```python
datos['descripción_local'] = datos['descripción_local'].str.replace(r'(\W|^)-(\W|$)', ' ', regex=True)
```

##### ✔️ ¿Qué hace esta expresión?

* Busca guiones que:

  * Están al inicio o fin de cadena (`^`, \`\$)
  * O están rodeados por caracteres no alfanuméricos (`\W`)

##### 🔍 Explicación:

* `(\W|^)`: carácter no alfanumérico o inicio de cadena.
* `-`: guion literal.
* `(\W|$)`: carácter no alfanumérico o fin de cadena.

---
### 🔎 **Conceptos clave de regex**

| Símbolo | Significado                                                  | Ejemplo o nota adicional         |
| ------- | ------------------------------------------------------------ | -------------------------------- |
| `[]`    | Conjunto de caracteres permitidos                            | `[abc]` coincide con 'a', 'b', 'c' |
| `^`     | Negación (dentro de `[]`) o inicio de cadena (fuera de `[]`) | `[^abc]` o `^Hola`               |
| `\W`    | Cualquier carácter que **no** sea alfanumérico               | Coincide con símbolos como `@` o `#` |
| `\s`    | Espacio en blanco                                            | Incluye espacios, tabs, saltos de línea |
| `$`     | Fin de cadena                                                | `mundo$` coincide con "Hola mundo" |
| `\|`     | “O” lógico                                                    | `promo\|descuento`                |
| `\`     | Escapa caracteres especiales                                 | `\.` busca un punto literal      |

---

### 🧠 **Métodos importantes en Pandas**

#### `str.replace(pat, repl, regex=True)`

* Reemplaza valores que coincidan con un patrón.
* `pat`: el patrón a buscar.
* `repl`: el valor nuevo.
* `regex=True`: indica que `pat` es una expresión regular.

#### `str.strip()`

* Elimina espacios al inicio y final de la cadena.
* Útil luego de aplicar `.replace()`.

---

### 💡 **Ejemplo práctico**

```python
import pandas as pd

texto = pd.Series(["¡Hola, mundo! 123. ¿Cómo estás?"])
texto_limpio = texto.str.replace('[^a-zA-Z0-9\s]', '', regex=True)

print(texto_limpio[0])  # Output: Holamundo 123 Cómoestás
```

---

### 📌 **Resumen**

* **Regex** permite definir patrones complejos para limpiar texto automáticamente.
* Es ideal para tareas de **preprocesamiento de texto**, fundamentales en **análisis de datos** y **NLP** (procesamiento de lenguaje natural).
* Usar métodos como `.str.replace()` con `regex=True` permite personalizar la limpieza.
* Los métodos `.apply()` y `.applymap()` también ayudan a aplicar funciones personalizadas a columnas o DataFrames completos.

---
## 🧩 ¿Qué son las Expresiones Regulares (Regex)?

**Regex** (del inglés *regular expressions*) es una **secuencia de caracteres especiales** que define un **patrón de búsqueda** dentro de un texto. Es una herramienta poderosa que permite:

* Buscar coincidencias en cadenas.
* Reemplazar fragmentos de texto.
* Extraer o validar información estructurada.
* Limpiar datos de forma automatizada.

---

## 🧪 Aplicaciones en Ciencia de Datos

### 🔹 **1. Limpieza de datos**

* **Eliminar símbolos no deseados** como `$`, `%`, `#`, etc.
* **Normalizar texto**, por ejemplo, convertir a minúsculas o eliminar espacios dobles.

```python
df['columna'] = df['columna'].str.replace('[^a-zA-Z0-9 ]', '', regex=True)
```

### 🔹 **2. Extracción de información**

* Extraer **números de teléfono**, **correos electrónicos**, **fechas**, etc., desde texto sin estructurar.

```python
# Buscar correos en una columna
df['email'] = df['texto'].str.extract(r'[\w\.-]+@[\w\.-]+\.\w+')
```

### 🔹 **3. Clasificación de texto**

* Detectar **patrones repetitivos** que indiquen si un correo es *spam*.
* Buscar palabras clave específicas en reseñas, publicaciones o mensajes.

```python
df['spam'] = df['mensaje'].str.contains(r'(gratis|oferta|haz clic aquí)', case=False)
```

---

## 🧠 Ventajas del uso de Regex en Ciencia de Datos

| Ventaja                        | Descripción                                                                                     |
| ------------------------------ | ----------------------------------------------------------------------------------------------- |
| 🔍 Búsqueda avanzada           | Permite identificar patrones complejos que un simple `.contains()` no podría.                   |
| ⚙️ Automatización              | Facilita la limpieza masiva de texto sin necesidad de bucles.                                   |
| 📊 Mejora del análisis textual | Ayuda a preprocesar datos antes de aplicar algoritmos de NLP o Machine Learning.                |
| 🔐 Validación de datos         | Puedes verificar si una cadena cumple con un formato (como una cédula, correo o código postal). |

---

## ✏️ Ejemplos útiles

| Objetivo                       | Regex                           | Descripción                                        |
|-------------------------------|----------------------------------|----------------------------------------------------|
| Eliminar caracteres especiales| `[^a-zA-Z0-9 ]`                  | Todo lo que no sea letra, número o espacio.        |
| Extraer dígitos               | `\d+`                            | Uno o más dígitos seguidos.                        |
| Detectar correos electrónicos| `[\w\.-]+@[\w\.-]+\.\w+`         | Coincide con correos electrónicos básicos.         |
| Palabras específicas          | `\b(promo|descuento)\b`         | Detecta palabras exactas "promo" o "descuento".    |

✅ **Notas**:

* Los símbolos `\b` indican **límites de palabra**, para que no detecte partes de otras palabras (por ejemplo, "promocionar").
* Todo está alineado para que se vea bien tanto en editores Markdown como en Jupyter Notebooks.
---
## 🧠 ¿Dónde se aplica Regex?

Las expresiones regulares (Regex) se utilizan ampliamente para buscar, validar, extraer o modificar cadenas de texto en diversas áreas. A continuación, se presentan algunos ejemplos comunes:

---

### 1. 🔍 **Consultas en bases de datos**

Regex puede usarse en motores de bases de datos compatibles para realizar búsquedas avanzadas.

```sql
SELECT * FROM filmes WHERE titulo REGEXP '^[era uma vez]';
```

**Explicación:**

* `^`: indica que la coincidencia debe comenzar al inicio de la cadena.
* `[era uma vez]`: esta notación está incorrecta para expresar “era una vez”. Aquí se está buscando títulos que empiecen con cualquiera de los caracteres `e`, `r`, `a`, etc.
  ✔️ **Forma correcta esperada**: `'^(era|uma|vez)'`

---

### 2. ✅ **Validación de entradas (Java)**

Regex es útil para validar correos electrónicos, contraseñas, números, etc.

```java
private void setEmail(String email) {
    String regex = "^[A-Za-z0-9+_.-]+@(.+)$";
    if (!email.matches(regex)) {
        throw new IllegalArgumentException("Email Inválido!");
    }
    this.email = email;
}
```

**Explicación:**

* `^[A-Za-z0-9+_.-]+`: permite letras, números y símbolos comunes antes del `@`.
* `@(.+)$`: garantiza que después del `@` haya al menos un carácter.

---

### 3. 🧾 **Extracción de datos (ejemplo: CPF brasileño)**

```regex
[0-9]{3}\.?[0-9]{3}\.?[0-9]{3}\-?[0-9]{2}
```

**Explicación:**

* `[0-9]{3}`: tres dígitos numéricos.
* `\.?`: punto opcional (el `\` escapa el punto).
* `\-?`: guion opcional.
* Esta expresión busca coincidencias como `123.456.789-00`.

---

### 4. 📊 **Procesamiento de datos (Ejemplo: Tableau)**

#### 🧩 a) `REGEXP_REPLACE(cadena, patrón, reemplazo)`

Reemplaza caracteres según un patrón.

```text
REGEXP_REPLACE([categoria_produto], '[0-9]|[-]|[_]', ' ')
```

**Objetivo:** Eliminar números, guiones y guiones bajos, reemplazándolos por espacios.

#### 🧪 b) `REGEXP_MATCH(cadena, patrón)`

Devuelve `TRUE` si la cadena coincide con el patrón, `FALSE` si no.

```text
REGEXP_MATCH([categoria], '([0-9])')
```

**Objetivo:** Verificar si hay al menos un dígito en el campo `categoria`.

#### 🧬 c) `REGEXP_EXTRACT(cadena, patrón)`

Extrae parte de la cadena que coincida con un patrón.

```text
REGEXP_EXTRACT([categoria_produto], '(\d+)')
```

**Objetivo:** Extraer el número de identificación (`id`) que aparece al inicio del texto (como `1-` en `1-agro_industria`).

---

## ✅ Resumen

| Aplicación                 | Herramienta/función                  | Descripción breve                                         |
| -------------------------- | ------------------------------------ | --------------------------------------------------------- |
| Consultas SQL              | `REGEXP`                             | Filtra registros por patrones de texto                    |
| Validación en código Java  | `String.matches(regex)`              | Verifica si una cadena cumple con el formato esperado     |
| Extracción en datos crudos | Regex manual o con herramientas      | Identifica patrones como números, fechas o correos        |
| Procesamiento en Tableau   | `REGEXP_REPLACE`, `MATCH`, `EXTRACT` | Limpia, verifica o extrae valores específicos en columnas |

---
# ✂️ Transformar textos en listas (Tokenización en Pandas)

La **tokenización** es el proceso de dividir una cadena de texto en unidades más pequeñas llamadas **tokens**, que suelen ser palabras, frases o símbolos.
En **ciencia de datos**, la tokenización es fundamental para preparar texto antes de análisis o modelado.

---

## 🔑 Conceptos Clave

| Concepto                          | Definición                                                                              |
| --------------------------------- | --------------------------------------------------------------------------------------- |
| **Tokenización**                  | Proceso de dividir texto en unidades más pequeñas (palabras, frases, símbolos).         |
| **Strings (cadenas)**             | Secuencias de caracteres que representan texto. En Pandas, se manejan con `Series.str`. |
| **Regex (Expresiones regulares)** | Patrones que permiten buscar, limpiar y manipular texto de forma flexible.              |

---

## 🛠️ Métodos Utilizados en Pandas

| Método                                | Función                                                                                        | Ejemplo                                     |
| ------------------------------------- | ---------------------------------------------------------------------------------------------- | ------------------------------------------- |
| `.str.split(sep)`                     | Divide el texto en una lista de tokens usando un separador (por defecto espacio).              | `"hola mundo".split()` → `['hola','mundo']` |
| `.str.replace(pat, repl, regex=True)` | Reemplaza partes de un texto según un patrón regex. Útil para eliminar caracteres no deseados. | `texto.str.replace('[{}"]','',regex=True)`  |

---

## ⚙️ Ejemplo práctico en Pandas

Supongamos que tenemos un DataFrame con una columna de descripciones:

```python
import pandas as pd

data = {'descripcion': ["Este es un ejemplo de frase con algunas palabras."]}
df = pd.DataFrame(data)

# Tokenización por espacios
df['descripcion_tokenizada'] = df['descripcion'].str.split()

print(df)
```

### ✅ Resultado:

| descripcion                                         | descripcion\_tokenizada                                                        |
| --------------------------------------------------- | ------------------------------------------------------------------------------ |
| "Este es un ejemplo de frase con algunas palabras." | \['Este', 'es', 'un', 'ejemplo', 'de', 'frase', 'con', 'algunas', 'palabras.'] |

---

## 🧹 Limpieza con Regex antes de tokenizar

Si el texto contiene **caracteres no deseados** como `{}`, `"` o puntuación, podemos limpiarlo primero:

```python
df['descripcion_limpia'] = df['descripcion'].str.replace('[{}"]', '', regex=True)
df['descripcion_tokenizada'] = df['descripcion_limpia'].str.split()
```

Esto genera una columna **limpia** y luego la **lista de tokens** sin caracteres especiales.

---

## 📌 Variantes de Tokenización

1. **Separación por espacios (default):**

   ```python
   df['columna'].str.split()
   ```

   → Divide en palabras por espacio.

2. **Separación por comas:**

   ```python
   df['columna'].str.split(',')
   ```

   → Útil si tenemos listas tipo `"python,pandas,numpy"`.

3. **Regex como separador:**

   ```python
   df['columna'].str.split('[,;.]')
   ```

   → Divide usando comas, punto y coma o punto.

---
## 📝 Apunte: Limpieza de texto con Regex en Pandas

### 🔹 Problema

Algunas columnas tienen texto extra dentro de paréntesis, por ejemplo:

```
A101 (blocoAP)
A102 (blocoAP)
```

y necesitamos eliminar esa parte.

---

### 🔹 Errores comunes

1. **Paréntesis en regex**
   Los `()` son grupos en regex, por eso se deben **escapar** con `\(` y `\)`.
   Ejemplo: `\(blocoAP\)` busca exactamente `(blocoAP)`.

2. **Uso de `\` en Python**
   En Python, la barra invertida también es especial.
   Para evitar problemas, usamos **raw strings** (`r''`).
   Ejemplo: `r'\(blocoAP\)'`.

3. **Espacios alrededor**
   En los datos aparece `" (blocoAP)"`, no solo `"(blocoAP)"`.
   Por eso conviene incluir el espacio en el patrón.

---

### 🔹 Solución

Código para eliminar `" (blocoAP)"` de la columna:

```python
datos2['apartamento'] = datos2['apartamento'].str.replace(r'\s*\(blocoAP\)', '', regex=True)
```

✅ Explicación del patrón:

* `\s*` → cero o más espacios antes.
* `\(blocoAP\)` → literal `(blocoAP)`.

---

### 🔹 Extra (más general)

Si quieres eliminar **cualquier cosa entre paréntesis**, usa:

```python
datos2['apartamento'] = datos2['apartamento'].str.replace(r'\s*\(.*?\)', '', regex=True)
```

👉 `.*?` significa “cualquier cosa” dentro de los paréntesis.

---

📌 **Resultado esperado**:

```
A101
A101
A102
A102
```

---
