# 🐼 Módulo 4 : Manipulación de los datos
---

# ➕ Crear Nuevas Columnas en un DataFrame de Pandas

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




