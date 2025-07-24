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
