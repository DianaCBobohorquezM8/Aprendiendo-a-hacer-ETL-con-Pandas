# 🐼 Módulo 4 : Leyendo  paginas en HTML y  XML 📁
---
# 🎬 Importando Páginas Web con Pandas

## 🎯 Caso de Uso: Recomendador de Películas

- **Definición**: Crear un recomendador de películas para una empresa.
- **Objetivo**: Obtener datos de películas desde una página web para analizarlos y usarlos en el sistema de recomendación.

---

## 🌐 Fuente de Datos

- **Origen**: Página de Wikipedia con una tabla de películas de los últimos 100 años.
- **Contenido útil**: título, año, director, productora, ranking, etc.
- **Motivo de elección**: contiene datos estructurados y accesibles públicamente.

---

## 🧪 Paso 1: Inspeccionar el Código Fuente

- **Herramienta**: Clic derecho → `Inspeccionar` (navegador).
- **Objetivo**: Verificar si los datos están en una **tabla HTML**.
- **Importancia**: La función `pd.read_html()` solo extrae datos de **tablas** en HTML.

---

## 📥 Paso 2: Importar la Tabla con `pd.read_html()`

```python
import pandas as pd

url = 'https://es.wikipedia.org/wiki/Lista_de_pel%C3%ADculas_m%C3%A1s_exitosas'
tablas = pd.read_html(url)
````

* **`pd.read_html()`**: función de Pandas que busca y extrae **todas las tablas HTML** de una página web.
* **Resultado**: devuelve una **lista de DataFrames**, uno por cada tabla encontrada.

---

## 🗂️ Paso 3: Seleccionar la Tabla Correcta

```python
peliculas = tablas[0]  # Ejemplo: seleccionar la primera tabla
```

* **Lista de tablas**: `tablas` es una lista ordenada.
* **Índice**: selecciona la tabla deseada usando su posición. *(Recuerda: los índices en Python inician en 0)*.
* Puedes imprimir las primeras filas para inspeccionar:

```python
peliculas.head()
```

---

## 🧠 Conceptos Clave

| Término              | Definición breve                                                      |
| -------------------- | --------------------------------------------------------------------- |
| **API**              | Interfaz que conecta sistemas y permite el intercambio de datos.      |
| **HTML**             | Lenguaje con el que se estructuran las páginas web.                   |
| **Inspeccionar**     | Herramienta del navegador para ver el código HTML.                    |
| **`pd.read_html()`** | Función de Pandas para leer tablas HTML y convertirlas en DataFrames. |
| **Lista (Python)**   | Estructura de datos que almacena elementos ordenados.                 |

---

## ✅ Conclusión

* Con `pd.read_html()`, puedes extraer fácilmente datos tabulados desde páginas web.
* Es una herramienta poderosa para proyectos como sistemas de recomendación, análisis histórico, estadísticas públicas, etc.
* Verifica siempre que los datos estén en formato **tabla HTML** antes de usar esta función.

---

## 🔗 Recursos

* [📘 Pandas: `read_html()` Documentation](https://pandas.pydata.org/docs/reference/api/pandas.read_html.html)
* [🌐 Wikipedia: Películas más exitosas](https://es.wikipedia.org/wiki/Anexo:Pel%C3%ADculas_m%C3%A1s_exitosas)
---
