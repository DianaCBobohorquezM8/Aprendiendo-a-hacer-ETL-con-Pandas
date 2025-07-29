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
