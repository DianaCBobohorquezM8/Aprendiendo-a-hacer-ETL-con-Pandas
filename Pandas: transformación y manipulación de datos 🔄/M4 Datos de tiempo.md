# 🐼 Módulo 4 : Datos de tiempo 🔄
---
# 📅 Manejo de Fechas y Horas en Python

## 🔹 Clase `datetime`

* Es una clase de Python que representa **fecha y hora** específicas.
* Permite trabajar con: año, mes, día, hora, minuto, segundo y microsegundo.
* También reconoce **días de la semana** (lunes, martes, etc.).
* Es fundamental para:

  * Calcular diferencias entre fechas.
  * Formatear fechas y horas.
  * Analizar datos de **series temporales**.

---

## 🔹 Uso en **Pandas**

Con la biblioteca **Pandas** se pueden realizar operaciones como:

* Convertir cadenas de texto a `datetime`.
* Filtrar datos por intervalos de tiempo.
* Agrupar datos por hora, día, mes o año.
* Manejar fechas de forma **eficiente en DataFrames**.

---

## 🔹 Biblioteca `datetime` (estándar de Python)

Proporciona clases para trabajar con fechas y horas:

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

📌 `date.today()` → devuelve únicamente la fecha (sin hora).

---

### ✅ Diferencia entre fechas

```python
import datetime

# Dos fechas
data_1 = datetime.date(2022, 1, 1)
data_2 = datetime.date(2023, 1, 1)

# Diferencia
diferencia = data_2 - data_1
print("Diferencia entre las dos fechas:", diferencia)
```

📌 Operaciones matemáticas con fechas:

* Resta → devuelve un objeto `timedelta` (número de días de diferencia).

---

## 🔹 Resumen

* `datetime.datetime` → Fecha + hora.
* `datetime.date` → Solo fecha.
* `datetime.timedelta` → Diferencia entre fechas.
* En **Pandas**, fechas se convierten fácilmente con `pd.to_datetime()`.

---
