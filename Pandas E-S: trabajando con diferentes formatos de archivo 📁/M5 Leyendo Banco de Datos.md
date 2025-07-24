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
## 🧠 Introducción a SQL

**SQL (Structured Query Language)** es un lenguaje usado para interactuar con bases de datos **relacionales**, permitiendo:

* 📥 Insertar
* 📝 Actualizar
* 🔍 Consultar
* 🗃️ Administrar datos

---

## 🧱 Cláusulas SQL Principales

Las **cláusulas** son los bloques de construcción de las sentencias SQL. Permiten **filtrar, ordenar, agrupar o limitar** los datos consultados.

| Cláusula   | Función                                           |
| ---------- | ------------------------------------------------- |
| `SELECT`   | Especifica las columnas a consultar               |
| `FROM`     | Indica la tabla desde la que se extraen los datos |
| `WHERE`    | Filtra los resultados según condiciones           |
| `ORDER BY` | Ordena los resultados (ascendente o descendente)  |
| `GROUP BY` | Agrupa los datos por una o más columnas           |
| `LIMIT`    | Limita el número de filas devueltas               |

---

## 🧪 Ejemplo SQL

```sql
SELECT nombre, apellido, salario
FROM empleados
WHERE departamento = 'ventas';
```

### 🔍 Análisis del ejemplo:

* `SELECT nombre, apellido, salario`: columnas que se quieren visualizar.
* `FROM empleados`: tabla origen de los datos.
* `WHERE departamento = 'ventas'`: condición que filtra solo los empleados del área de ventas.

---
## 🧠 Lectura y Escritura de SQL con Pandas

### 🔧 1. `read_sql()`: Leer resultados de una consulta SQL

```python
pd.read_sql(sql, con)
```

Este método te permite **ejecutar una consulta SQL** y obtener el resultado directamente en un DataFrame de Pandas.

#### 🔹 Parámetros importantes:

* `sql`: la **consulta SQL** (puede ser una cadena o un objeto `sqlalchemy.text()`).
* `con`: el **motor de conexión** a la base de datos (por ejemplo, un `engine` de SQLAlchemy).

#### ✅ Ventajas:

* Permite ejecutar consultas complejas con `JOIN`, `WHERE`, `GROUP BY`, etc.
* Carga automáticamente los resultados como un DataFrame, listo para análisis.

#### 🧪 Ejemplo:

```python
from sqlalchemy import text

consulta = text("SELECT nombre, salario FROM empleados WHERE departamento = 'ventas'")
df = pd.read_sql(consulta, con=engine.connect())
```

---

### 📚 2. `read_sql_table()`: Leer una tabla completa

```python
pd.read_sql_table(table_name, con, columns=None)
```

Este método se usa para **cargar una tabla completa de una base de datos SQL** a un DataFrame.

#### 🔹 Parámetros importantes:

* `table_name`: nombre de la tabla a leer.
* `con`: el motor de conexión (`engine`).
* `columns` *(opcional)*: una lista con las columnas que deseas importar.

#### ✅ Ventajas:

* Rápido para cargar tablas completas.
* Útil para exploración o análisis inicial.

#### 🧪 Ejemplo:

```python
df = pd.read_sql_table('clientes', con=engine, columns=['nombre', 'correo'])
```

---

### 💾 3. `to_sql()`: Guardar un DataFrame como tabla en SQL

```python
df.to_sql(name, con, if_exists='fail', index=True)
```

Este método **exporta un DataFrame a una base de datos SQL** como una nueva tabla.

#### 🔹 Parámetros importantes:

* `name`: nombre de la tabla en la base de datos.
* `con`: motor de conexión (`engine`).
* `if_exists`:

  * `'fail'`: lanza error si la tabla ya existe.
  * `'replace'`: borra la tabla existente y la reemplaza.
  * `'append'`: agrega los datos al final de la tabla existente.
* `index`: si deseas incluir el índice del DataFrame como una columna.

#### ✅ Ventajas:

* Muy útil después de limpiar o transformar datos en Pandas.
* Permite actualizar la base de datos con nuevos registros desde Python.

#### 🧪 Ejemplo:

```python
df.to_sql('empleados_nuevo', con=engine, if_exists='replace', index=False)
```

---

## ⚙️ Extras Técnicos

### 🧱 `engine` de SQLAlchemy

Para que todo funcione, necesitas un **motor de conexión**, que se crea así:

```python
from sqlalchemy import create_engine

engine = create_engine('sqlite:///mi_base_de_datos.db')
```

Este motor se pasa a todos los métodos (`read_sql`, `read_sql_table`, `to_sql`).

---

### 📦 `text()` de SQLAlchemy

Cuando usas una cadena SQL con variables o condiciones, es buena práctica convertirla a `text`:

```python
from sqlalchemy import text

consulta = text("SELECT * FROM empleados WHERE salario > 3000")
```

Esto le dice a SQLAlchemy que debe tratar la consulta como un texto SQL.

---

## 🧩 Resumen de Métodos

| Método             | ¿Qué hace?                                          | ¿Cuándo usarlo?                                |
| ------------------ | --------------------------------------------------- | ---------------------------------------------- |
| `read_sql()`       | Ejecuta una consulta SQL                            | Cuando necesitas filtrar, unir o agrupar datos |
| `read_sql_table()` | Carga una tabla completa como DataFrame             | Cuando necesitas todos los datos de una tabla  |
| `to_sql()`         | Guarda un DataFrame como tabla en una base de datos | Para almacenar datos procesados desde Pandas   |

---
# 📦 Actualizando un Banco de Datos

## 🔍 ¿Qué se aprende?

Cómo realizar operaciones básicas en una base de datos usando SQL y leer los resultados en **Python** con `SQLAlchemy` y `Pandas`.

---

## 🛠️ Crear Consultas SQL

### 🔹 Seleccionar todos los registros

```sql
SELECT * FROM clientes;
```

### 🔹 Borrar un registro

```sql
DELETE FROM clientes WHERE id_cliente = 58804;
```

### 🔹 Actualizar un valor

```sql
UPDATE clientes SET grado_de_estudio = 'nivel superior' WHERE id_cliente = 58808;
```

---

## ⚙️ Ejecutar la Consulta con SQLAlchemy

### 1. 🔌 Conectar a la base de datos

```python
from sqlalchemy import create_engine

engine = create_engine('sqlite:///:memory:')
conexion = engine.connect()
```

> Se usa SQLite en memoria para practicar sin guardar datos en disco.

### 2. 📄 Envolver la consulta con `text()`

```python
from sqlalchemy import text

consulta_sql = text("SELECT * FROM clientes;")
```

### 3. ▶️ Ejecutar la consulta

```python
conexion.execute(consulta_sql)
```

---

## 📥 Leer datos con Pandas

### Usar `read_sql()` para traer los resultados

```python
import pandas as pd

df = pd.read_sql(consulta_sql, conexion)
print(df)
```

### Luego puedes acceder a los datos con:

```python
df.loc[0]
df['nombre']
```

---

## 🧪 Ejemplo Completo

```python
import pandas as pd
from sqlalchemy import create_engine, text

# Crear motor de base de datos en memoria
engine = create_engine('sqlite:///:memory:')
conexion = engine.connect()

# Crear tabla
conexion.execute(text("""
    CREATE TABLE clientes (
        id_cliente INTEGER PRIMARY KEY,
        nombre VARCHAR(50),
        grado_de_estudio VARCHAR(50)
    );
"""))

# Insertar datos
conexion.execute(text("""
    INSERT INTO clientes (id_cliente, nombre, grado_de_estudio) VALUES
    (58804, 'Ana Pérez', 'intermedio'),
    (58805, 'Juan Gómez', 'superior'),
    (58808, 'Luisa Torres', 'intermedio');
"""))

# Ejecutar consulta
consulta_sql = text("SELECT * FROM clientes;")
df = pd.read_sql(consulta_sql, conexion)
print(df)

# Cerrar conexión
conexion.close()
```

---

## ✅ Resumen de pasos

| Paso                   | Acción                                |
| ---------------------- | ------------------------------------- |
| 1️⃣ Conectar a la base | `create_engine()` + `connect()`       |
| 2️⃣ Escribir SQL       | SELECT, DELETE, UPDATE con `text()`   |
| 3️⃣ Ejecutar SQL       | `conexion.execute(text(...))`         |
| 4️⃣ Leer en Pandas     | `pd.read_sql()` devuelve un DataFrame |
| 5️⃣ Analizar datos     | Acceso con `.loc[]`, `.iloc[]`, etc.  |

---
