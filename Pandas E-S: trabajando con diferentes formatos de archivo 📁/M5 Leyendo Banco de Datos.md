# 🐼 Módulo 5 : Leyendo Banco de Datos 📁
---
# 🏗️ Creando un Banco de Datos Local con SQLAlchemy

## 🧠 Conceptos clave

### 🔸 SQL (Structured Query Language)
Lenguaje estructurado para ejecutar consultas en una base de datos.  
**Puede aplicarse a archivos CSV, Excel o sistemas como SQLite.**

### 🔸 SQLAlchemy
Biblioteca de Python para interactuar con bases de datos SQL.  
Permite ejecutar consultas y administrar estructuras directamente desde Python.

### 🔸 SQLite
Sistema de gestión de bases de datos relacional.  
**Ligero y fácil de usar**, ideal para crear bancos de datos locales.

---

## ⚙️ Componentes principales de SQLAlchemy

### 1. `create_engine()`
- **Función**: Crea el "motor" que permite conectar y operar con una base de datos.
- **Uso común**:
    ```python
  from sqlalchemy import create_engine
  engine = create_engine('sqlite:///:memory:')
  ````

**Analogía**: 🧱 Como construir los cimientos de un edificio.
  Sin motor, no hay conexión con la base de datos.

---

### 2. `MetaData`

* **Función**: Almacena la información estructural de las tablas: nombres, columnas, tipos.
* **Uso común**:

  ```python
  from sqlalchemy import MetaData
  metadata = MetaData()
  ```
* **Analogía**: 📐 Como un plano de construcción: muestra cómo está organizada la base de datos.

---

### 3. `Table`

* **Función**: Permite definir, consultar y manipular directamente una tabla de la base de datos.
* **Uso común**:

  ```python
  from sqlalchemy import Table, Column, Integer, String
  users = Table('users', metadata,
                Column('id', Integer, primary_key=True),
                Column('name', String))
  ```
* **Analogía**: 🔑 Como tener las llaves para acceder a cualquier sala de datos (tabla).

---

### 4. `inspect()`

* **Función**: Investiga la base de datos para mostrarte sus tablas y columnas.
* **Uso común**:

  ```python
  from sqlalchemy import inspect
  inspector = inspect(engine)
  inspector.get_table_names()
  ```
* **Analogía**: 🕵️ Como un detective que te dice qué hay dentro del edificio (base de datos).

---

### 5. `text()`

* **Función**: Convierte una consulta SQL en un formato ejecutable por Python.
* **Uso común**:

  ```python
  from sqlalchemy import text
  conn = engine.connect()
  conn.execute(text("SELECT * FROM users"))
  ```
* **Analogía**: 🌐 Como un traductor que convierte consultas SQL en lenguaje que Python puede entender.

---

## ✅ Resumen gráfico

| Componente      | Función principal                            | Analogía                  |
| --------------- | -------------------------------------------- | ------------------------- |
| `create_engine` | Crea la conexión a la base de datos          | Cimientos del edificio    |
| `MetaData`      | Define la estructura de las tablas           | Plano del edificio        |
| `Table`         | Permite trabajar directamente con las tablas | Llaves de cada sala       |
| `inspect`       | Investiga la base de datos                   | Detective o investigador  |
| `text`          | Convierte consultas SQL en objetos Python    | Traductor de SQL a Python |

---
# 🗂️ Bases de Datos 

## 🧾 ¿Qué es una base de datos?
Un sistema que **almacena, organiza y recupera información** de forma estructurada y eficiente.  
Se utiliza en muchos campos como la gestión empresarial, la ciencia, la tecnología, etc.

### ✅ Beneficios
- Aumenta la eficiencia y precisión de las operaciones.
- Facilita el manejo y análisis de grandes volúmenes de datos.

---

## 🔍 Tipos de bases de datos

| Tipo | Descripción | Ejemplo de uso |
|------|-------------|----------------|
| **Relacionales** | Organizan los datos en **tablas con filas y columnas**. | MySQL, PostgreSQL, SQLite |
| **No relacionales (NoSQL)** | Usan estructuras como documentos, grafos o pares llave-valor. | MongoDB, Redis, Neo4j |

---

## 🐍 Bases de datos en Python

Python permite interactuar con múltiples sistemas de bases de datos, como:

- **Relacionales**: SQLite, MySQL, PostgreSQL, Oracle
- **No relacionales**: MongoDB, Cassandra, etc.

### 🧩 Módulos útiles
- `sqlite3`: Integrado en Python. Ideal para bases de datos ligeras.
- `SQLAlchemy`: Biblioteca ORM que permite usar objetos Python en lugar de escribir SQL directamente.

---

## 🛠️ SQLAlchemy: Ventajas principales

| Característica | Beneficio |
|----------------|-----------|
| ORM (Object Relational Mapper) | Interactúas con la base de datos usando clases y objetos Python. |
| Abstracción del SQL | Menos errores y código más limpio. |
| Consultas complejas | Posible extraer datos fácilmente de grandes volúmenes. |
| Compatible con varios motores | SQLite, PostgreSQL, MySQL, etc. |

> ⚙️ Está instalado por defecto en **Google Colab** mediante SQLite, por lo que es ideal para prototipos y prácticas.

📚 **Consulta oficial**:  
👉 [Documentación de SQLAlchemy](https://docs.sqlalchemy.org/)

---
# 📝 Escribir en una base de datos con Pandas y SQLAlchemy

## 📁 1. Importar datos desde un archivo CSV

- Se utiliza la función `read_csv()` de **Pandas** para leer archivos `.csv`.
- Los datos se cargan en un **DataFrame**, una estructura tabular similar a una hoja de cálculo o una tabla SQL.

🔄 **Analogía**: El archivo CSV es una lista desordenada de ingredientes.  
Pandas actúa como un chef que organiza esos ingredientes en una tabla bien estructurada.

---

## 🛠️ 2. Crear una tabla SQL con `to_sql()`

- Se usa el método `to_sql()` de Pandas para exportar un DataFrame a una tabla SQL.
- Es necesario un **motor (engine)** de SQLAlchemy que conecte Python con la base de datos.

🔄 **Analogía**: Como guardar una tabla de Excel en una base de datos para hacer análisis avanzados.

---

## 🔍 3. Verificar la tabla con un inspector

- SQLAlchemy ofrece un **Inspector** para comprobar la existencia y estructura de las tablas.
- Permite revisar columnas, índices, claves, etc.

---

## 🧠 Conceptos clave

| Término      | Definición |
|--------------|------------|
| **Engine**   | Objeto de SQLAlchemy que actúa como puente entre Python y una base de datos específica. |
| **SQLAlchemy** | Biblioteca que facilita la conexión y manipulación de bases de datos SQL desde Python. |
| **Inspector** | Objeto que permite explorar la estructura de la base de datos (tablas, columnas, etc.). |

---

## 📊 4. Realizar consultas SQL

- Una vez exportados, puedes consultar los datos directamente con SQL.
- Puedes hacer filtros, agrupamientos, cálculos y reportes.

🔄 **Analogía**: Es como preguntar a una base de datos:  
"¿Cuántos clientes tienen más de 30 años?" o  
"¿Cuál es el ingreso promedio en cierta ciudad?"

---

## 🧪 Ejemplo de flujo completo

```python
import pandas as pd
from sqlalchemy import create_engine, inspect

# 1. Leer CSV
df = pd.read_csv("clientes.csv")

# 2. Crear engine (con SQLite en este ejemplo)
engine = create_engine("sqlite:///mi_base_de_datos.db")

# 3. Exportar a tabla SQL
df.to_sql("clientes", con=engine, if_exists="replace", index=False)

# 4. Verificar la tabla
inspector = inspect(engine)
print(inspector.get_table_names())
````

---
## 🔍 `get_table_names()` en SQLAlchemy

### 📌 ¿Qué es?

Es un método del objeto `inspector` en SQLAlchemy.

### ✅ ¿Qué hace?

Retorna una **lista con los nombres de todas las tablas** que existen dentro de la base de datos conectada mediante un `engine`.

### 📅 ¿Cuándo se usa?

* Para **verificar las tablas existentes** en una base de datos.
* Después de crear una nueva tabla con `to_sql()` para confirmar que fue registrada correctamente.
* Para **explorar** la estructura de una base de datos desconocida.

---

### 💻 Ejemplo de uso:

```python
from sqlalchemy import create_engine, inspect

# Crear un engine para conectarse a la base de datos (en memoria en este caso)
engine = create_engine('sqlite:///:memory:')

# Crear un inspector a partir del engine
inspector = inspect(engine)

# Obtener la lista de nombres de las tablas
table_names = inspector.get_table_names()

# Imprimir la lista de tablas
print(table_names)
```

### 📝 Notas:

* Si no se han creado tablas todavía, `table_names` será una **lista vacía**: `[]`.
* Puedes usar esta función después de usar `df.to_sql()` para confirmar que la tabla fue creada.

---
