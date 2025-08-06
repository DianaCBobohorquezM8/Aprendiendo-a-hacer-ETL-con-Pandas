# 📈 Módulo 3 : Personalizando gráficos con Matplotlib 📈
---
# 🎨 Estilos en Matplotlib

Matplotlib permite aplicar diferentes **estilos visuales** a los gráficos para adaptarlos a distintas necesidades de presentación.

---

## 🔎 Ver estilos disponibles

Para listar todos los estilos incluidos en Matplotlib:

```python
import matplotlib.pyplot as plt

print(plt.style.available)
```

📌 Ejemplo de salida:

```python
['Solarize_Light2', 'bmh', 'classic', 'dark_background', 'fast', 
 'fivethirtyeight', 'ggplot', 'grayscale', 'seaborn-v0_8', 
 'seaborn-v0_8-darkgrid', 'seaborn-v0_8-pastel', 
 'seaborn-v0_8-whitegrid', 'tableau-colorblind10']
```

---

## 📌 Guardar configuración predeterminada

Cuando importamos Matplotlib, se cargan estilos por defecto.
Para **guardar la configuración inicial** y poder restaurarla después:

```python
IPython_default = plt.rcParams.copy()
```

---

## ⭐ Usando un estilo globalmente

Podemos aplicar un estilo a **todos los gráficos** del notebook:

```python
plt.style.use('fivethirtyeight')
```

Ejemplo con estilo *FiveThirtyEight*:

```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots(figsize=(8, 4))
ax.plot(datos_col['Año'], datos_col['Inmigrantes'])
ax.set_title('Inmigración de colombianos hacia Canadá\n1980 a 2013', 
             fontsize=20, loc='left')
ax.set_ylabel('Número de Inmigrantes', fontsize=14)
ax.set_xlabel('Año', fontsize=14)
ax.yaxis.set_tick_params(labelsize=12)
ax.xaxis.set_tick_params(labelsize=12)
ax.xaxis.set_major_locator(plt.MultipleLocator(5))
plt.show()
```

🎨 Este estilo produce gráficos **limpios, modernos, con líneas gruesas y colores vibrantes**.

---

## 🔄 Restaurar estilo predeterminado

Si después queremos quitar el estilo aplicado:

```python
plt.rcParams.update(IPython_default)
```

---

## 🎯 Usar estilo en un bloque específico

Si queremos aplicar un estilo **solo en un bloque de código**:

```python
with plt.style.context('fivethirtyeight'):
    fig, ax = plt.subplots(figsize=(8, 4))
    ax.plot(datos_col['Año'], datos_col['Inmigrantes'])
    ax.set_title('Inmigración de colombianos hacia Canadá\n1980 a 2013', 
                 fontsize=20, loc='left')
    ax.set_ylabel('Número de Inmigrantes', fontsize=14)
    ax.set_xlabel('Año', fontsize=14)
    ax.yaxis.set_tick_params(labelsize=12)
    ax.xaxis.set_tick_params(labelsize=12)
    ax.xaxis.set_major_locator(plt.MultipleLocator(5))
    plt.show()
```

📌 En este caso, el estilo **solo afecta dentro del bloque `with`**, y luego se vuelve automáticamente al estilo anterior.

---

¿Quieres que te arme un **cuadro comparativo visual** con ejemplos del mismo gráfico en 3 estilos distintos (*classic*, *ggplot* y *fivethirtyeight*) para ver la diferencia?
