# 🐼 Módulo 4 : Datos de tiempo 🔄
---
# 📅  Clase `datetime` 

## 🔹Manejo de Fechas y Horas en Python

* Representa una **fecha y hora específicas**.
* Permite trabajar con: año, mes, día, hora, minuto, segundo y microsegundo.
* Reconoce **días de la semana**.
* Es fundamental para:

  * Calcular diferencias entre fechas.
  * Formatear fechas y horas.
  * Analizar **series temporales**.

---

## 🔹 Uso en **Pandas**

Con **Pandas** se pueden:

* Convertir cadenas a `datetime`.
* Filtrar por intervalos de tiempo.
* Agrupar por hora, día, mes o año.
* Manejar fechas en **DataFrames** de forma eficiente.

---

## 🔹 Biblioteca `datetime` (Python estándar)

### ✅ Fecha y hora actual

```python
import datetime
ahora = datetime.datetime.now()
print("Fecha y hora actual:", ahora)
```

📌 `datetime.now()` → crea un objeto con la fecha y hora actuales.

---

### ✅ Solo la fecha de hoy

```python
import datetime
hoy = datetime.date.today()
print("Fecha de hoy:", hoy)
```

📌 `date.today()` → devuelve solo la fecha.

---

### ✅ Diferencia entre fechas

```python
import datetime
data_1 = datetime.date(2022, 1, 1)
data_2 = datetime.date(2023, 1, 1)

diferencia = data_2 - data_1
print("Diferencia:", diferencia)
```

📌 La resta devuelve un objeto `timedelta`.

---

## 📌 Resumen rápido

* `datetime.datetime` → Fecha + hora
* `datetime.date` → Solo fecha
* `datetime.timedelta` → Diferencia de tiempo
* `pd.to_datetime()` → Conversión en Pandas

---

# 📅 `datetime` en Python (nivel avanzado)

---

## 1. Objetos **conscientes vs ingenuos**

* **Conscientes (aware):**

  * Incluyen zona horaria (`tzinfo`).
  * Representan un instante **exacto**.
  * Ej: `UTC`, `EST`.

* **Ingenuos (naive):**

  * No incluyen zona horaria.
  * Interpretación depende del programa.
  * Son más simples, pero menos precisos.

---

## 2. Manejo de zonas horarias

```python
from datetime import datetime, timezone
ahora = datetime.now(timezone.utc)
print(ahora)
```

* Clase concreta: `timezone`
* Alias: `datetime.timezone.utc`

---

## 3. Constantes del módulo

* `MINYEAR = 1`
* `MAXYEAR = 9999`
* `UTC = datetime.timezone.utc` (Python 3.11+)

---

## 4. Tipos principales

| Clase       | Representa            | Atributos principales       |
| ----------- | --------------------- | --------------------------- |
| `date`      | Fecha                 | `year, month, day`          |
| `time`      | Hora                  | `hour, min, sec, µsec`      |
| `datetime`  | Fecha + hora          | Todos los anteriores        |
| `timedelta` | Diferencia            | `days, sec, µsec`           |
| `tzinfo`    | Zona horaria (base)   | Usada en `time`, `datetime` |
| `timezone`  | Zona horaria concreta | Offset a UTC                |

---

## 5. Propiedades comunes

✅ Inmutables
✅ Hashables (se usan como claves en diccionarios)
✅ Compatibles con `pickle`

---

## 6. Determinar si un objeto es **consciente**

* `date` → siempre ingenuo
* `datetime` o `time` → conscientes si:

  1. `obj.tzinfo != None`
  2. `obj.tzinfo.utcoffset(obj) != None`

---

## 7. Objetos `timedelta`

```python
from datetime import timedelta
d = timedelta(days=2, hours=5, minutes=30)
print(d)  # 2 days, 5:30:00
```

✔ Conversión automática:

* 1 min → 60 s
* 1 h → 3600 s
* 1 sem → 7 días

✔ Normalización:

* `0 <= µs < 1,000,000`
* `0 <= s < 86,400`
* `-999999999 <= d <= 999999999`

---

## 8. Relaciones entre clases

```
object
 ├── timedelta
 ├── tzinfo
 │    └── timezone
 ├── time
 ├── date
 │    └── datetime
```

---
# 📅 Manejo de columnas `datetime` en Pandas

---

## 🔹 1. Transformar datos al tipo `datetime`

### 📌 Carga de datos

* **Concepto:** Se cargan datos desde archivos externos (ej. JSON) a un DataFrame.
* **Método clave:** `pd.read_json()`

```python
import pandas as pd
data_dt = pd.read_json('inmuebles_disponibles.json')
```

---

### 📌 Exploración de datos

* **Concepto:** Entender la estructura y tipos de datos del DataFrame.
* **Métodos clave:**

```python
data_dt.head()   # Muestra primeras 5 filas
data_dt.info()   # Tipos de datos y valores no nulos
```

---

### 📌 Transformación a `datetime`

* **Problema:** Las fechas suelen cargarse como `object` (strings).
* **Solución:** Convertir con `pd.to_datetime()`.

```python
data_dt['fecha'] = pd.to_datetime(data_dt['fecha'])
```

Con formato específico:

```python
data_dt['Fecha de venta'] = pd.to_datetime(
    data_dt['Fecha de venta'],
    format='%d/%m/%Y'
)
```

📌 **Analogía de relojes:**

* `pd.read_json()` → abrir la caja de relojes.
* `.head()` / `.info()` → inspeccionar los relojes.
* `pd.to_datetime()` → sacar relojes de la bolsa plástica (strings) y dejarlos listos.
* Asignación → guardar los relojes ya ajustados en la caja (DataFrame).

---

## 🔹 2. Manipular columnas `datetime`

### 📌 Variables de tiempo

* Columnas `datetime` permiten usar métodos para extraer año, mes, día, hora, etc.

---

### 📌 Agrupación por meses

* Sirve para identificar **tendencias o estacionalidad**.

```python
# Extraer año-mes
data_dt['año_mes'] = data_dt['fecha'].dt.strftime('%Y-%m')

# Agrupar por año-mes y contar disponibilidad
reporte = data_dt.groupby('año_mes')['disponible'].sum()
print(reporte)
```

---

### 📌 Métodos clave

* `.dt` → acceder a propiedades `datetime`.
* `.strftime('%Y-%m')` → formatear fechas.
* `.groupby()` → agrupar por columnas.
* `.sum()` → sumar valores (ej. contar disponibles).

---

### 📌 Ejemplo práctico

```python
# Transformar fecha
data_dt['fecha'] = pd.to_datetime(data_dt['fecha'])

# Agrupar por año y mes
reporte_tiempo = (
    data_dt
    .groupby(data_dt['fecha'].dt.strftime('%Y-%m'))['disponible']
    .sum()
)

print(reporte_tiempo)
```

---

## 🔹 3. Informes de tiempo

* **Qué permiten:**

  * Ver disponibilidad de propiedades a lo largo del tiempo.
  * Detectar **patrones estacionales** (ej. mayor demanda en ciertos meses).
  * Apoyar decisiones (precios, marketing, oferta).

---

✅ **Resumen final:**

1. Cargar datos → `pd.read_json()`
2. Explorar → `.head()`, `.info()`
3. Convertir fechas → `pd.to_datetime()`
4. Extraer año/mes → `.dt.strftime('%Y-%m')`
5. Agrupar datos → `.groupby()`
6. Generar reportes de tiempo → `.sum()`

---
# 📅 Fechas y Horas en Python (`datetime`)

## 🔹 1. Formatear fechas en cadenas

### 📌 Usando `.format()`

```python
data_em_texto = '{}/{}/{}'.format(data_atual.day, data_atual.month, data_atual.year)
# Resultado → 1/3/2018
```

⚠️ Problema: días y meses < 10 no muestran el prefijo `0`.

```python
# Intento con ceros fijos
data_em_texto = '0{}/0{}/{}'.format(data_atual.day, data_atual.month, data_atual.year)
# Resultado → 010/010/2018 (incorrecto)
```

---

### 📌 Usando `.strftime()` (solución correcta ✅)

```python
data_em_texto = data_atual.strftime('%d/%m/%Y')
print(data_em_texto)  # 01/03/2018
```

📌 **Ventaja:** Control total sobre el formato con códigos (`%d`, `%m`, `%Y`, etc.).

---

## 🔹 2. Manejo de `datetime` (fecha + hora)

```python
from datetime import datetime
data_e_hora_atuais = datetime.now()
print(data_e_hora_atuais.strftime('%d/%m/%Y %H:%M'))
# Ejemplo → 01/03/2018 12:30
```

✔ Permite manejar **fecha y hora simultáneamente**.
✔ Se usa `.now()` en lugar de `.today()`.

---

## 🔹 3. Convertir cadenas en fechas (`strptime`)

```python
from datetime import datetime

data_em_texto = '01/03/2018 12:30'
data_e_hora = datetime.strptime(data_em_texto, '%d/%m/%Y %H:%M')
print(data_e_hora)
```

👉 Convierte **string → objeto datetime**.

---

## 🔹 4. Problema de zonas horarias

El resultado puede variar entre máquinas porque cada una tiene configuraciones distintas de **zona horaria**.

✅ Solución: fijar la zona horaria con `timezone` o librerías externas como **pytz**.

---

## 🔹 5. Zona horaria con `timezone` y `timedelta`

```python
from datetime import datetime, timezone, timedelta

data_e_hora_atuais = datetime.now()
diferenca = timedelta(hours=-3)  # UTC-3 (São Paulo)
fuso_horario = timezone(diferenca)

data_sao_paulo = data_e_hora_atuais.astimezone(fuso_horario)
print(data_sao_paulo.strftime('%d/%m/%Y %H:%M'))
# Resultado → 01/03/2018 12:30
```

⚡ Nota: `timedelta(hours=-3)` corrige la diferencia horaria respecto a UTC.

---

## 🔹 6. Zona horaria con **pytz** (recomendado)

Instalación:

```bash
pip install pytz
```

Uso:

```python
from datetime import datetime
from pytz import timezone

data_e_hora_atuais = datetime.now()
fuso_horario = timezone('America/Sao_Paulo')
data_sao_paulo = data_e_hora_atuais.astimezone(fuso_horario)

print(data_sao_paulo.strftime('%d/%m/%Y %H:%M'))
```

📌 Con `pytz.all_timezones` puedes listar todas las zonas horarias disponibles.

---

## 🔹 7. Códigos comunes en `strftime`

| Código | Significado         | Ejemplo |
| ------ | ------------------- | ------- |
| `%d`   | Día del mes (01-31) | 01      |
| `%m`   | Mes (01-12)         | 03      |
| `%Y`   | Año con siglo       | 2018    |
| `%H`   | Hora (00-23)        | 12      |
| `%M`   | Minuto (00-59)      | 30      |

---

## ✅ Resumen final

1. **Formatear fechas** → usar `.strftime()`.
2. **Convertir string → fecha** → usar `.strptime()`.
3. **Manejar zona horaria** → usar `timezone` + `timedelta` o librería `pytz`.
4. **Evitar errores entre máquinas** → siempre fijar zona horaria explícita.

---
