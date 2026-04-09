# 1.2. Agregaciones de datos

## Uso de `agg` en Pandas

La función `agg` en pandas permite aplicar múltiples funciones de agregación a una o más columnas de un DataFrame.

**Sintaxis básica**

Por el momento nos centraremos en comprender como aplicar una función de agregación a una sola columna.

```python
df['columna'].agg(funcion1)
```

para aplicar múltiples funciones de agregación una columna de un DataFrame se utiliza:

```python
df['columna'].agg([funcion1, funcion2, funcion3])
```
---
**Ejemplo de uso**

```python
import pandas as pd

# Crear un DataFrame de ejemplo
df = pd.DataFrame({
    'Edad': [29, 35, 23, 32, 27],
    'Salario': [50000, 70000, 45000, 65000, 60000]
})

# Aplicar funciones de agregación
df_agg['Edad'] = df.agg(['mean', 'min', 'max'])
print(df_agg)
```
---
## Funciones acumulativas en Pandas: `cumsum()`, `cummax()`, `cummin()`, `cumprod()`

Pandas proporciona funciones acumulativas que permiten calcular valores acumulativos sobre una columna específica de un DataFrame o Serie.

---

**1. `cumsum()`: Suma acumulativa**

Calcula la suma acumulativa de los valores en una columna.

```python
df['Salario Acumulado'] = df['Salario'].cumsum()
print(df)
```

Ejemplo de salida:

```
    Nombre  Edad  Salario  Salario Acumulado
0     Ana    29   50000              50000
1  Carlos    35   70000             120000
2 Beatriz    23   45000             165000
3   David    32   65000             230000
```
---

**2. `cummax()`: Máximo acumulativo**

Encuentra el valor máximo acumulado en la columna.

```python
df['Salario Máximo Acumulado'] = df['Salario'].cummax()
print(df)
```

Ejemplo de salida:

```
    Nombre  Edad  Salario  Salario Máximo Acumulado
0     Ana    29   50000                       50000
1  Carlos    35   70000                       70000
2 Beatriz    23   45000                       70000
3   David    32   65000                       70000
```

---

**3. `cummin()`: Mínimo acumulativo**

Encuentra el valor mínimo acumulado en la columna.

```python
df['Salario Mínimo Acumulado'] = df['Salario'].cummin()
print(df)
```

Ejemplo de salida:

```
    Nombre  Edad  Salario  Salario Mínimo Acumulado
0     Ana    29   50000                       50000
1  Carlos    35   70000                       50000
2 Beatriz    23   45000                       45000
3   David    32   65000                       45000
```

---

**4. `cumprod()`: Producto acumulativo**

Calcula el producto acumulativo de los valores en una columna.

```python
df['Salario Producto Acumulado'] = df['Salario'].cumprod()
print(df)
```

Ejemplo de salida:

```
    Nombre  Edad  Salario  Salario Producto Acumulado
0     Ana    29   50000                        50000
1  Carlos    35   70000                  3500000000
2 Beatriz    23   45000             157500000000000
3   David    32   65000       10237500000000000000
```

---

**En resumen**

- `cumsum()` se usa para calcular la suma acumulativa.
- `cummax()` obtiene el valor máximo acumulado hasta ese punto.
- `cummin()` devuelve el mínimo acumulado.
- `cumprod()` calcula el producto acumulado.

Estas funciones son útiles en análisis financiero, estadísticas y análisis de tendencias dentro de conjuntos de datos.

---

## Uso de `value_counts()` en Pandas

La función `value_counts()` permite contar la cantidad de ocurrencias de cada valor único en una columna de un DataFrame o en una Serie.

**Sintaxis básica**

```python
Serie.value_counts(normalize=False, sort=True, ascending=False, bins=None, dropna=True)
```

**Parámetros clave**

- `normalize`: Si es `True`, devuelve las proporciones en lugar de los conteos.
- `sort`: Si es `True`, los valores se ordenan por frecuencia de mayor a menor.
- `ascending`: Si es `True`, ordena en orden ascendente.
- `bins`: Si se proporciona un número, divide los datos en intervalos y cuenta cuántos valores caen en cada uno.
- `dropna`: Si es `True`, excluye valores nulos (`NaN`).

---

Ejemplo de uso

```python
df = pd.DataFrame({
    'Categoría': ['A', 'B', 'A', 'C', 'B', 'A', 'C', 'C', 'B', 'A']
})

conteo = df['Categoría'].value_counts()
print(conteo)
```

Salida esperada:
```
A    4
B    3
C    3
Name: Categoría, dtype: int64
```

---

Uso de `value_counts()` con `normalize=True`

```python
proporcion = df['Categoría'].value_counts(normalize=True)
print(proporcion)
```

Salida esperada:
```
A    0.4
B    0.3
C    0.3
Name: Categoría, dtype: float64
```

---

**En resumen**

- `value_counts()` es útil para analizar la distribución de valores en una columna.
- Permite contar valores absolutos o proporciones (`normalize=True`).
- Se puede ordenar de manera ascendente o descendente según necesidad.
- El parámetro `bins` ayuda a agrupar valores numéricos en intervalos.

---

## Uso de `groupby()` en Pandas

La función `groupby()` en pandas permite agrupar datos según una o más columnas y aplicar funciones de agregación sobre los grupos.

**Sintaxis básica**

```python
df.groupby(by)[['columna']].funcion()
```

Ejemplo de uso

```python
df = pd.DataFrame({
    'Departamento': ['Ventas', 'Ventas', 'IT', 'IT', 'RRHH', 'RRHH'],
    'Empleado': ['Ana', 'Carlos', 'Beatriz', 'David', 'Elena', 'Fernando'],
    'Salario': [50000, 70000, 65000, 62000, 48000, 51000]
})

# Agrupar por departamento y calcular el salario promedio
df_grouped = df.groupby('Departamento')[['Salario']].mean()
print(df_grouped)
```

Salida esperada:
```
            Salario
Departamento        
IT          63500.0
RRHH        49500.0
Ventas      60000.0
```

---

**Otras funciones comunes con `groupby()`**

- `sum()`: Suma de valores por grupo.
- `count()`: Número de elementos en cada grupo.
- `max()`: Valor máximo en cada grupo.
- `min()`: Valor mínimo en cada grupo.
- `agg()`: Aplicar múltiples funciones de agregación a la vez.

---

**Uso de `groupby()` con `agg()`**

```python
df_grouped = df.groupby('Departamento').agg({'Salario': ['mean', 'sum', 'max', 'min']})
print(df_grouped)
```

Salida esperada:
```
            Salario                  
               mean    sum    max    min
Departamento                             
IT          63500.0  127000  65000  62000
RRHH        49500.0   99000  51000  48000
Ventas      60000.0  120000  70000  50000
```

---

**En resumen**

- `groupby()` es esencial para realizar análisis agrupados.
- Se puede aplicar con funciones de agregación (`sum()`, `mean()`, `count()`, etc.).
- `agg()` permite aplicar múltiples funciones de agregación a la vez.

---

## Uso de `pivot_table()` en Pandas

La función `pivot_table()` en pandas permite resumir y reorganizar datos en un formato tabular, similar a una tabla dinámica en Excel.

**Sintaxis básica**

```python
pd.pivot_table(df, values, index, columns, aggfunc='mean', fill_value=None)
```

**Parámetros clave**
- `values`: La columna cuyos valores se quieren resumir.
- `index`: La(s) columna(s) que se usarán como índices de la tabla.
- `columns`: La(s) columna(s) que se usarán como encabezados de columna.
- `aggfunc`: La función de agregación a aplicar (por defecto, `mean`). Se pueden usar funciones como `sum`, `count`, `min`, `max`, etc.
- `fill_value`: Valor para rellenar valores faltantes (por defecto, `None`).

---

Ejemplo de uso

```python
import pandas as pd

# Crear un DataFrame de ejemplo
df = pd.DataFrame({
    'Departamento': ['Ventas', 'Ventas', 'IT', 'IT', 'RRHH', 'RRHH'],
    'Empleado': ['Ana', 'Carlos', 'Beatriz', 'David', 'Elena', 'Fernando'],
    'Género': ['F', 'M', 'F', 'M', 'F', 'M'],
    'Salario': [50000, 70000, 65000, 62000, 48000, 51000]
})

# Crear una tabla dinámica que muestre el salario promedio por departamento y género
pivot = pd.pivot_table(df, values='Salario', index='Departamento', columns='Género', aggfunc='mean')
print(pivot)
```

Salida esperada:
```
Género             F        M
Departamento                
IT         65000.0  62000.0
RRHH       48000.0  51000.0
Ventas     50000.0  70000.0
```

---

**Uso de `pivot_table()` con múltiples funciones de agregación**

```python
pivot_multi = pd.pivot_table(df, values='Salario', index='Departamento', columns='Género', aggfunc=['mean', 'sum'])
print(pivot_multi)
```

Salida esperada:
```
            mean                 sum          
Género         F        M       F       M
Departamento                              
IT       65000.0  62000.0   65000   62000
RRHH     48000.0  51000.0   48000   51000
Ventas   50000.0  70000.0   50000   70000
```

---

**En resumen**

- `pivot_table()` es útil para resumir datos de manera flexible.
- Se pueden aplicar múltiples funciones de agregación.
- Permite manejar valores nulos con `fill_value`.

Estas herramientas son esenciales para el análisis exploratorio de datos en ciencia de datos.

[`Ejemplo`](./code/1.2-aggregating_data.ipynb)