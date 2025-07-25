# 🐼 Módulo 2 : Datos numéricos  🔄
---
# 🧬 Transformación de Listas en el DataFrame con `explode()`

## 📌 ¿Por qué transformar listas en filas?

Cuando trabajamos con **datos reales**, es común encontrar columnas donde las celdas contienen **listas de elementos**. Por ejemplo, una propiedad puede tener múltiples **comodidades** como `["WiFi", "TV", "Piscina"]`, todas en una sola celda. Para **analizar individualmente cada comodidad**, necesitamos **separarlas en filas**.

---

## 🔧 Método: `.explode()`

### 🔍 ¿Qué hace?

Convierte cada elemento de una lista contenida en una celda en **una nueva fila** del DataFrame, **repitiendo el resto de los valores de la fila original**.

### 🧠 ¿Por qué es útil?

* Facilita análisis como: cuántas propiedades tienen cierta comodidad.
* Permite visualizar la frecuencia de elementos individuales.
* Prepara los datos para **agrupamientos y filtros más detallados**.

### 🧪 Ejemplo:

```python
# Explota la columna 'comodidades' que contiene listas
datos = datos.explode('comodidades')
```

---

## 🔄 Resetear el índice con `.reset_index()`

Después de usar `.explode()`, el índice del DataFrame puede quedar **desordenado** o duplicado.

### ✔ Solución:

```python
datos.reset_index(inplace=True, drop=True)
```

* `inplace=True`: modifica el DataFrame original.
* `drop=True`: elimina el índice anterior (evita que se cree una columna con los índices viejos).

---

## 🧾 Inspección de tipos con `.info()`

Para asegurarte de que los datos están limpios y listos para análisis, es fundamental revisar los **tipos de cada columna**:

```python
datos.info()
```

Este comando devuelve:

* Nombres de columnas.
* Tipo de dato (`int64`, `float64`, `object`, etc.).
* Cantidad de valores no nulos.

---

## 🗃️ Descripción de las columnas en `datos_hosting.json`

| Columna                | Descripción                              |
| ---------------------- | ---------------------------------------- |
| `evaluacion_general`   | Puntuación media del alojamiento.        |
| `experiencia_local`    | Actividades ofrecidas en la estancia.    |
| `max_hospedes`         | Número máximo de huéspedes permitidos.   |
| `descripcion_local`    | Descripción de la propiedad.             |
| `descripcion_vecindad` | Descripción del vecindario.              |
| `cantidad_baños`       | Número total de baños.                   |
| `cantidad_cuartos`     | Número de habitaciones disponibles.      |
| `cantidad_camas`       | Número de camas en la propiedad.         |
| `modelo_cama`          | Tipo o modelo de cama ofrecida.          |
| `comodidades`          | Lista de comodidades (WiFi, TV, etc.).   |
| `cuota_deposito`       | Tarifa mínima de depósito por seguridad. |
| `cuota_limpieza`       | Tarifa cobrada por limpieza.             |
| `precio`               | Precio base diario por la estancia.      |

---

## 💡 Puntos clave del proceso

| Paso                         | Descripción                                                 |
| ---------------------------- | ----------------------------------------------------------- |
| Detectar columnas con listas | Usualmente tipo `object` que contienen listas en cada fila. |
| Aplicar `.explode()`         | Convierte cada elemento de la lista en una fila nueva.      |
| Usar `.reset_index()`        | Reorganiza los índices para evitar errores posteriores.     |
| Revisar `.info()`            | Verifica estructura y tipos de datos del DataFrame.         |

---

## 🧭 Ejemplo completo

```python
# Explota la columna de listas
datos = datos.explode('comodidades')

# Resetea el índice para reorganizar el DataFrame
datos.reset_index(inplace=True, drop=True)

# Inspecciona la estructura del DataFrame
datos.info()
```

---
