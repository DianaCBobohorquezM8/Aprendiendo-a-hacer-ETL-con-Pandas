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
