# 1.1. Transformación de datos 

## Ordenamiento y Filtrado

En análisis de datos, es común necesitar ordenar los datos en función de una o más columnas. La función `sort_values` de pandas nos permite realizar este ordenamiento de manera sencilla y eficiente.

**Sintaxis de `sort_values`**

```python
DataFrame.sort_values(by, axis=0, ascending=True, inplace=False, kind='quicksort', na_position='last')
```

## Parámetros clave:

- `by`: Nombre de la columna (o lista de columnas) por la que se ordenará el DataFrame.
- `ascending`: Booleano o lista de valores booleanos. `True` (por defecto) ordena en orden ascendente; `False`, en orden descendente.
- `inplace`: Si es `True`, modifica el DataFrame original; si es `False` (por defecto), devuelve un nuevo DataFrame ordenado.
- `na_position`: Define la posición de los valores nulos (`'first'` para colocarlos al inicio, `'last'` para colocarlos al final).
- `kind`: Tipo de algoritmo de ordenamiento (`'quicksort'`, `'mergesort'`, `'heapsort'`, `'stable'`).

---

**Ejemplos de Uso**

1. Ordenamiento por una sola columna

```python
import pandas as pd

# Crear un DataFrame de ejemplo
df = pd.DataFrame({
    'Nombre': ['Ana', 'Carlos', 'Beatriz', 'David'],
    'Edad': [29, 35, 23, 32],
    'Salario': [50000, 70000, 45000, 65000]
})

# Ordenar por la columna 'Edad'
df_ordenado = df.sort_values(by='Edad')
print(df_ordenado)
```

2. Ordenamiento en orden descendente

```python
# Ordenar por 'Salario' de mayor a menor
df_desc = df.sort_values(by='Salario', ascending=False)
print(df_desc)
```

3. Ordenamiento por múltiples columnas

```python
# Ordenar por 'Edad' ascendente y luego por 'Salario' descendente
df_multi = df.sort_values(by=['Edad', 'Salario'], ascending=[True, False])
print(df_multi)
```

4. Manejo de valores nulos en el ordenamiento

```python
df_con_nulos = pd.DataFrame({
    'Nombre': ['Ana', 'Carlos', 'Beatriz', 'David', 'Elena'],
    'Edad': [29, None, 23, 32, 27]
})

# Ordenar colocando los valores nulos al inicio
df_nulos_first = df_con_nulos.sort_values(by='Edad', na_position='first')
print(df_nulos_first)
```

**Consideraciones Adicionales**

- Para ordenamientos estables (manteniendo el orden relativo de elementos con el mismo valor), usa `kind='stable'`.
- Si `inplace=True`, el DataFrame se modificará directamente sin necesidad de reasignarlo a una nueva variable.

## Crear nuevas columnas en un DataFrame

Es posible agregar nuevas columnas a un DataFrame de diversas maneras en pandas.

1. Asignando valores directamente

```python
df['Bonos'] = [5000, 7000, 4000, 6000]
print(df)
```

2. Usando cálculos basados en otras columnas

```python
df['Salario Total'] = df['Salario'] + df['Bonos']
print(df)
```

3. Agregar una columna con valores constantes

```python
df['Pais'] = 'México'
print(df)
```

- Se pueden agregar columnas asignando listas o valores constantes.
- `apply` es útil para cálculos personalizados.
- Es posible realizar cálculos con columnas existentes para crear nuevas columnas.

[`Ejemplo`](./code/1.1.-sort_filter.ipynb) - [`Reto`](./code/1.1.-sort_filter_exercise.ipynb)