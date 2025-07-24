# 🐼 Módulo 4 : Leyendo  paginas en HTML y  XML 📁
---
# 🌐 ¿Qué es HTML?

**HTML** (*HyperText Markup Language* o *Lenguaje de Marcado de Hipertexto*) es el **lenguaje estándar** para **estructurar** el contenido de una página web.

---

## 🧱 Estructura básica de un documento HTML

```html
<html>
  <head>
    <title>Título de la página</title>
  </head>
  <body>
    <!-- Aquí va el contenido visible -->
  </body>
</html>
````

* `<html>`: etiqueta raíz del documento.
* `<head>`: contiene metadatos, título y enlaces a estilos/scripts.
* `<body>`: contiene el contenido visible de la página web.

---

## 🧩 Principales etiquetas HTML

| Etiqueta        | Función                        |
| --------------- | ------------------------------ |
| `<h1>` a `<h6>` | Títulos y subtítulos           |
| `<p>`           | Párrafos                       |
| `<ul>`, `<li>`  | Listas no ordenadas            |
| `<ol>`, `<li>`  | Listas ordenadas               |
| `<img>`         | Insertar imágenes              |
| `<a>`           | Crear enlaces                  |
| `<table>`       | Crear tablas                   |
| `<tr>`          | Fila de tabla                  |
| `<th>`          | Encabezado de celda de tabla   |
| `<td>`          | Celda de contenido de la tabla |

---

## 🧪 Atributos Comunes

Los atributos permiten **agregar información adicional** a una etiqueta.

| Atributo | Uso                    | Ejemplo                                |
| -------- | ---------------------- | -------------------------------------- |
| `src`    | Fuente de imagen       | `<img src="imagen.jpg">`               |
| `href`   | Enlace                 | `<a href="https://ejemplo.com">Ir</a>` |
| `alt`    | Texto alternativo      | `<img alt="Descripción">`              |
| `target` | Abrir en nueva pestaña | `<a href="..." target="_blank">`       |

---

## 📌 Resumen

* HTML define **la estructura** de las páginas web.
* Utiliza **etiquetas** para agrupar y representar contenido.
* Los **atributos** modifican el comportamiento o apariencia de los elementos.
* Es el **primer paso** en el desarrollo web, junto con CSS y JavaScript.

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
# 📝 Exportando DataFrames a HTML y CSV

Exportar tus datos te permite compartir, visualizar o reutilizar tus análisis fácilmente. Aquí te muestro cómo hacerlo en **HTML** y **CSV**.

---

## 📄 Exportar a HTML con `to_html()`

### 🔧 ¿Qué hace?
Convierte un DataFrame en una **tabla HTML**.

### 🧪 Sintaxis básica:
```python
df.to_html('mi_tabla.html', index=False, classes='table table-striped')
````

### 🧰 Parámetros útiles:

| Parámetro           | Función                           |
| ------------------- | --------------------------------- |
| `index=False`       | No incluye el índice en la tabla  |
| `classes='...'`     | Aplica clases CSS para estilo     |
| `escape=True/False` | Escapa caracteres HTML especiales |

### ✅ Ventajas:

* El archivo generado puede abrirse directamente en un navegador.
* Permite aplicar estilos visuales fácilmente con clases CSS.

---

## 📁 Exportar a CSV con `to_csv()`

### 🔧 ¿Qué hace?

Convierte un DataFrame en un archivo **CSV (Comma Separated Values)**.

### 🧪 Sintaxis básica:

```python
df.to_csv('mi_archivo.csv', sep=';', encoding='utf-8')
```

### 🧰 Parámetros útiles:

| Parámetro          | Función                                        |
| ------------------ | ---------------------------------------------- |
| `sep=';'`          | Define el separador (coma, punto y coma, etc.) |
| `encoding='utf-8'` | Define la codificación de caracteres           |
| `quotechar='"'`    | Carácter para encerrar campos con comillas     |

---

## 🧠 Buenas prácticas

* **🔍 Revisa los archivos exportados** antes de enviarlos o compartirlos.
* Asegúrate de que los datos estén bien estructurados y legibles.
* Verifica la codificación si vas a compartir con personas en otros sistemas operativos.

---
# 🗃️ Introducción a XML

## 📝 ¿Qué es XML?

*XML (eXtensible Markup Language)** es un lenguaje de marcación que permite **describir, estructurar y almacenar datos** de forma estandarizada. Su sintaxis se basa en **etiquetas (tags)** que definen elementos y atributos.

---

## 🧱 Estructura básica de un documento XML

1. **Declaración XML**  
   Define la versión y la codificación del documento.
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
    ````

2. **Elemento raíz**
   Contiene a todos los demás elementos del archivo.
   Ejemplo: `<animales>...</animales>`

3. **Elementos secundarios**
   Anidados dentro del elemento raíz. Pueden tener texto o más elementos.
   Ejemplo: `<animal>`

4. **Atributos**
   Proporcionan información adicional sobre los elementos.
   Ejemplo: `nombre="Mel"`

---

## 📦 Ejemplo completo

   ```xml
<?xml version="1.0" encoding="UTF-8"?>
<animales>
  <animal nombre="Mel" tipo="perro" color="marron"/>
  <animal nombre="Vick" tipo="gato" color="blanco"/>
</animales> 
   ```

* `<animales>` → Elemento raíz.
* `<animal>` → Elemento secundario.
* `nombre`, `tipo`, `color` → Atributos.
* `"Mel"` y `"Vick"` → Valores dentro de los atributos.

---

## ✅ Ventajas de XML

* Legible por humanos y máquinas.
* Portátil entre sistemas y plataformas.
* Ideal para estructurar datos jerárquicos.

---
## 📂 Lectura y Escritura de Archivos XML

**🧾Estructura de un archivo XML
Un archivo XML está organizado en forma jerárquica con etiquetas anidadas. Ejemplo:

```xml
<Data>
  <Row>
    <index>1</index>
    <poster_link>https://example.com/poster1.jpg</poster_link>
    <series_title>The Shawshank Redemption</series_title>
  </Row>
  <Row>
    <index>2</index>
    <poster_link>https://example.com/poster2.jpg</poster_link>
    <series_title>The Dark Knight</series_title>
  </Row>
</Data>
````

* `<Data>`: Etiqueta raíz.
* `<Row>`: Representa una fila de datos.
* Las etiquetas internas son las columnas.

---

## 📥 Leer archivos XML con `read_xml()`

### 🔧 ¿Qué hace?

Convierte un archivo XML en un **DataFrame**.

### 🧪 Ejemplo:

```python
import pandas as pd

datos_imdb = pd.read_xml("IMDB Top 1000 XML.xml")
print(datos_imdb.head(3))
```

🔹 `read_xml(filepath)`: Lee un XML desde la ruta especificada.
🔹 `head(n)`: Muestra las primeras *n* filas del DataFrame.

---

## 📤 Escribir archivos XML con `to_xml()`

### 🔧 ¿Qué hace?

Convierte un DataFrame en un archivo XML.

### 🧪 Ejemplo:

```python
datos_imdb.to_xml("peliculas_imdb.xml")
```

🔹 `to_xml(filepath)`: Guarda el DataFrame como XML en la ruta dada.

---

## ✅ Resumen rápido

| Acción       | Método       | Descripción                                  |
| ------------ | ------------ | -------------------------------------------- |
| Leer XML     | `read_xml()` | Convierte archivo XML a DataFrame            |
| Escribir XML | `to_xml()`   | Convierte DataFrame a archivo XML            |
| Vista previa | `head(n)`    | Muestra las primeras *n* filas del DataFrame |

---

