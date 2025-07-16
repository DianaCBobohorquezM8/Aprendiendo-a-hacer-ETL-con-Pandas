# 🐼 Módulo 4 : Manipulación de los datos
---

# ➕ Crear Nuevas Columnas en un DataFrame

En análisis de datos es común **crear nuevas columnas** derivadas de operaciones matemáticas, transformaciones u otras columnas existentes. Pandas lo hace fácil y flexible. 💪

---

## 🛠️ Pasos para Crear una Nueva Columna

1. **Selecciona el DataFrame**
   - Asegúrate de tener cargado tu DataFrame.
   - Ejemplo de nombre: `datos`

2. **Asigna un nombre a la nueva columna**
   - Debe ser una cadena de texto.
   - Ejemplo: `"valor mensual"`, `"alquiler_en_dolares"`

3. **Realiza la operación deseada**
   - Puede ser una suma, resta, división, concatenación, función, etc.

4. **Asigna los valores usando la sintaxis correcta**

```python
datos["nueva_columna"] = operación_sobre_columnas_existentes
````

---

## 🧮 Ejemplo 1: Suma de columnas

Crear una columna llamada `"valor mensual"` sumando las columnas `"alquiler"` y `"condominio"`:

```python
datos["valor mensual"] = datos["alquiler"] + datos["condominio"]
```

📌 Cada fila del DataFrame obtendrá un nuevo valor en `"valor mensual"` como resultado de la suma.

---

## 💵 Ejemplo 2: Conversión de moneda

Crear una columna `"alquiler_en_dolares"` asumiendo un tipo de cambio de 1 dólar = 5 reales:

```python
datos["alquiler_en_dolares"] = datos["alquiler"] / 5
```

✅ Este tipo de cálculo es útil para transformar unidades o hacer análisis internacionales.

---

## 📌 Notas Importantes

* Puedes aplicar cualquier operación que funcione con Series de Pandas.
* Las nuevas columnas se crean automáticamente si no existen.
* Si la columna ya existe, se **sobrescribirá** con los nuevos valores.
* Puedes usar funciones personalizadas o condicionales con `.apply()` o `np.where()` si necesitas lógica más compleja.

  🧠 Consejito
  Usa nombres de columnas **claros y descriptivos**. Esto facilita entender tu DataFrame más adelante.
---
# 🧱 Creación de Nuevas Columnas 

En Pandas, podemos crear nuevas columnas con base en operaciones matemáticas, concatenación de strings o funciones personalizadas. Esta práctica es esencial para enriquecer nuestros datos y facilitar análisis posteriores 📊.

---

## 🧾 ¿Por qué crear nuevas columnas?

✅ Para combinar información de varias columnas.  
✅ Para aplicar transformaciones a datos existentes.  
✅ Para añadir nuevas variables de análisis.  
✅ Para preparar los datos antes de exportarlos o visualizarlos.

---

## 🛠️ ¿Cómo se hace?

```python
df["nueva_columna"] = operación_o_función
````

Por ejemplo:

```python
datos["valor mensual"] = datos["alquiler"] + datos["condominio"]
```

📌 Esto suma los valores de las columnas `"alquiler"` y `"condominio"` y los guarda en una nueva columna `"valor mensual"`.

---

## 💬 Concatenación de Texto: Crear descripciones

Podemos generar frases útiles para reportes o visualizaciones:

```python
datos["Descripción"] = (
    datos["Tipo"] + " en la colonia " + datos["Colonia"] +
    " con " + datos["Habitaciones"].astype(str) + " habitaciones y " +
    datos["Garaje"].astype(str) + " garajes."
)
```

🗣️ Esto crea oraciones como:

```
"Casa en la colonia Roma con 3 habitaciones y 1 garajes."
```

---

## 🔁 ¿Por qué usamos `.astype(str)`?

Cuando combinamos texto (`str`) con números (`int`, `float`), necesitamos convertir los números a texto primero.

```python
datos["Habitaciones"].astype(str)
```

📌 Esto evita errores como:

```
TypeError: can only concatenate str (not "int") to str
```

---

## 🎯 Ejemplo Completo

```python
datos["Descripción"] = (
    datos["Tipo"] + " en " + datos["Colonia"] +
    ", " + datos["Ciudad"] + " — " +
    datos["Habitaciones"].astype(str) + " hab., " +
    datos["Baños"].astype(str) + " baños, " +
    datos["Garaje"].astype(str) + " garajes."
)
```

🔎 Resultado:

```
"Departamento en Chapinero, Bogotá — 2 hab., 2 baños, 1 garajes."
```

---

## 👀 Verificando que todo funcione

| Método                        | Propósito                                     |
| ----------------------------- | --------------------------------------------- |
| `df.head()`                   | Muestra las primeras filas del DataFrame 🧾   |
| `df.iloc[500]`                | Muestra todos los valores de la fila 500 🔍   |
| `df.iloc[500]['Descripción']` | Muestra solo la descripción de la fila 500 🧠 |

---
## 📥 Exportar el resultado

Cuando ya tengas la columna lista y desees guardar los cambios:

```python
datos.to_csv("datos_modificados.csv", index=False)
```

📄 También puedes usar:

* `to_excel("archivo.xlsx")`
* `to_json("archivo.json")`
* `to_xml("archivo.xml")` 🆕

---

## ✅ Resumen Visual

```python
# Crear columna con operaciones matemáticas
df["total"] = df["precio"] + df["impuestos"]

# Crear columna con concatenación de strings
df["resumen"] = df["producto"] + " - " + df["categoría"]

# Crear columna condicional
df["nivel"] = df.apply(lambda fila: "Alto" if fila["ventas"] > 10000 else "Bajo", axis=1)
```

🧠 Cada una de estas formas nos permite manipular y enriquecer nuestros datos de manera clara y poderosa.

---





