# 🐼 Módulo 3 : Tratamiento y filtrado de los datos
---

# 🚫 Manejo de Valores Nulos (NaN)

En muchas bases de datos reales encontrarás **valores nulos (NaN)**. Estos indican datos faltantes o desconocidos, y deben ser tratados correctamente para evitar errores en el análisis.

---

## 🔍 Paso 1: Verificar valores nulos con `isnull()`

El método `DataFrame.isnull()` devuelve un DataFrame del mismo tamaño con valores **booleanos**:

- `True` → valor nulo (`NaN`)
- `False` → valor no nulo

### ✅ Ejemplo:

```python
df.isnull()
````

👆 Esto muestra una tabla de `True`/`False` indicando la presencia de valores nulos por celda.

---

## 🔢 Paso 2: Contar valores nulos con `sum()`

Puedes contar cuántos valores nulos hay por columna:

```python
df.isnull().sum()
```

🧠 Como `True` se interpreta como `1`, esta suma indica cuántos **NaN** tiene cada columna.

### 📌 Resultado esperado:

| Columna | Valores nulos |
| ------- | ------------- |
| ciudad  | 2             |
| tipo    | 0             |
| valor   | 4             |

---

## 🧽 Paso 3: Reemplazar valores nulos con `fillna()`

Usa `fillna(valor)` para reemplazar todos los `NaN` por un valor específico:

```python
df = df.fillna(0)
```

📌 Esto reemplaza todos los nulos por `0` en todo el DataFrame.

### 🚨 Importante

* Si no usas `inplace=True` o reasignas el resultado, **el DataFrame original no se modifica**.

```python
df.fillna(0, inplace=True)  # Cambios permanentes
```

---

## 🧠 Recapitulación

| Función             | Qué hace                             |
| ------------------- | ------------------------------------ |
| `df.isnull()`       | Devuelve `True` donde hay `NaN`      |
| `df.isnull().sum()` | Cuenta cuántos `NaN` hay por columna |
| `df.fillna(x)`      | Reemplaza todos los `NaN` por `x`    |

---

## 🎯 Tip: Reemplazar con la media o la moda

También puedes reemplazar valores nulos con estadísticas como la media, mediana o moda:

```python
df["columna"].fillna(df["columna"].mean(), inplace=True)
```

Esto es útil cuando no quieres reemplazar con `0`, sino con un valor representativo del conjunto.

---

## ✅ Conclusión

* Detectar y tratar valores nulos es esencial para un análisis limpio y preciso 🧹
* Usa `isnull()` y `sum()` para inspeccionar
* Usa `fillna()` para limpiar
* ¡Hazlo de forma permanente con `inplace=True` o reasignando el resultado! 🔄

💡 Una base de datos sin nulos es más fácil de visualizar, analizar y modelar correctamente.

---
# 🧹 Lidiando con Datos Nulos

El tratamiento de **datos nulos (NaN)** es fundamental en cualquier análisis de datos, ya que pueden afectar negativamente la calidad y la precisión de los resultados.

---

## ⚠️ ¿Por qué es importante?

Cuando un conjunto de datos contiene valores nulos, pueden surgir problemas como:

- 📉 **Sesgo en los resultados**
- 🔍 **Pérdida de precisión**
- ❌ Algunos modelos estadísticos **no funcionan con NaN**
- 💡 Decisiones incorrectas si no se tratan adecuadamente

Por eso, **identificar y manejar correctamente los NaN** es clave para obtener análisis confiables.

---

## 🧰 Métodos para tratar datos nulos en Pandas

### 1. 🗑️ Eliminar datos nulos: `dropna()`

Elimina las filas o columnas que contienen **al menos un valor nulo**.

### ✅ Ejemplos:

```python
df.dropna()              # Elimina filas con NaN
df.dropna(axis=1)        # Elimina columnas con NaN
````

### 🧠 Cuándo usarlo:

* Si los datos faltantes son pocos
* Si eliminar no afecta el análisis

---

### 2. 🧯 Llenar datos nulos: `fillna()`

Permite **reemplazar los NaN** por un valor específico o por valores vecinos.

### ✅ Ejemplos:

```python
df.fillna(0)                        # Reemplaza con 0
df.fillna(df["col"].mean())        # Reemplaza con la media
df.fillna(method="ffill")          # Reemplaza con el valor anterior (forward fill)
df.fillna(method="bfill")          # Reemplaza con el valor siguiente (backward fill)
```

| Método     | Descripción                               |
| ---------- | ----------------------------------------- |
| `"ffill"`  | Usa el valor anterior (forward fill)      |
| `"bfill"`  | Usa el valor siguiente (backward fill)    |
| Valor fijo | Reemplaza por un valor definido (ej. `0`) |

---

### 3. 🔁 Interpolar datos: `interpolate()`

Calcula valores intermedios usando técnicas de **interpolación matemática**.

### ✅ Ejemplo:

```python
df["col"].interpolate()
```

🧠 Ideal para datos numéricos y series temporales.

---

## 🧠 Elección adecuada

| Estrategia      | Cuándo usarla                                  |
| --------------- | ---------------------------------------------- |
| `dropna()`      | Pocos NaN, se pueden eliminar sin perder valor |
| `fillna()`      | Datos categóricos o numéricos con valor fijo   |
| `interpolate()` | Series numéricas con continuidad lógica        |

---
# 🧹 Limpieza de Datos en Pandas: Identificación y Eliminación de Registros Inconsistentes

La limpieza de datos es una de las tareas más importantes en el análisis de datos. Aquí aprenderás cómo identificar y eliminar registros inconsistentes utilizando `df.query()`, `.index`, `drop()`, y cómo verificar los cambios con `head()` y `sample()`.

---

## 🕵️‍♀️ 1. Identificación de Registros Inconsistentes

Usamos `df.query()` para buscar registros **anómalos** como apartamentos con valor de **alquiler o condominio igual a cero**.

### 📌 Ejemplo:

```python
inconsistentes = df.query("valor == 0 or condominio == 0")
print(inconsistentes)
````

---

## 🧾 2. Crear un Filtro con Índices

Extraemos los índices de estos registros para luego eliminarlos:

```python
indices = inconsistentes.index
```

🔍 Esto devuelve una lista con los índices de las filas que cumplen con la condición.

---

## ❌ 3. Eliminación de Registros con `drop()`

Eliminamos las filas utilizando el parámetro `axis=0` (eje de las filas) y `inplace=True` para aplicar el cambio directamente:

```python
df.drop(indices, axis=0, inplace=True)
```

---

## 🧹 4. Eliminación de Columnas Innecesarias

Ya que todos los registros son del mismo tipo (por ejemplo, "departamento"), podemos eliminar la columna `"tipo"`:

```python
df.drop("tipo", axis=1, inplace=True)
```

---

## 🔍 5. Verificación del Resultado

Utilizamos `head()` para ver las primeras filas, y `sample()` para ver una muestra aleatoria del DataFrame:

```python
df.head()     # Verifica los primeros registros
df.sample(5)  # Muestra aleatoria de 5 filas
```

---

## 🧠 Funciones y Conceptos Clave

| Función        | Descripción                                           |
| -------------- | ----------------------------------------------------- |
| `df.query()`   | Filtra filas según condiciones lógicas                |
| `.index`       | Devuelve los índices de las filas seleccionadas       |
| `df.drop()`    | Elimina filas (`axis=0`) o columnas (`axis=1`)        |
| `inplace=True` | Aplica los cambios directamente al DataFrame original |
| `df.head()`    | Muestra las primeras 5 filas del DataFrame            |
| `df.sample(n)` | Muestra una selección aleatoria de `n` filas          |

---

## 🧪 Código completo de ejemplo:

```python
# 1. Identificar registros con valores inconsistentes
inconsistentes = df.query("valor == 0 or condominio == 0")

# 2. Obtener los índices de estos registros
indices = inconsistentes.index

# 3. Eliminar los registros
df.drop(indices, axis=0, inplace=True)

# 4. Eliminar la columna innecesaria
df.drop("tipo", axis=1, inplace=True)

# 5. Verificar los cambios
print(df.head())
print(df.sample(5))
```

---



