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
