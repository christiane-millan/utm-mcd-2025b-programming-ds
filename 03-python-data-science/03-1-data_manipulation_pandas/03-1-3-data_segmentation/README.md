# 1.3.  Segmentación de datos

# Manipulación de Datos con Pandas

## El conjunto de datos de bandas de rock, revisado

```python
import pandas as pd

bands = pd.DataFrame({
    "nombre": ["Metallica", "Queen", "Nirvana", "The Beatles", "Pink Floyd", "AC/DC", "Led Zeppelin"],
    "género": ["Heavy Metal", "Rock Clásico", "Grunge", "Rock Clásico", "Rock Progresivo", "Hard Rock", "Rock Clásico"],
    "color_icónico": ["Negro", "Blanco", "Negro", "Blanco", "Negro", "Negro", "Negro"],
    "álbumes_publicados": [11, 15, 3, 12, 15, 17, 9],
    "años_activos": [40, 50, 7, 10, 30, 50, 12]
})

print(bands)
```
**Salida esperada:**
```
         nombre         género color_icónico  álbumes_publicados  años_activos
0    Metallica    Heavy Metal         Negro                  11            40
1       Queen  Rock Clásico         Blanco                  15            50
2     Nirvana        Grunge         Negro                   3             7
3  The Beatles  Rock Clásico         Blanco                  12            10
4  Pink Floyd  Rock Progresivo         Negro                  15            30
5       AC/DC     Hard Rock         Negro                  17            50
6  Led Zeppelin  Rock Clásico         Negro                   9            12
```

## `.columns` y `.index`

```python
bands.columns
```
**Salida esperada:**
```
Index(['nombre', 'género', 'color_icónico', 'álbumes_publicados', 'años_activos'], dtype='object')
```

```python
bands.index
```
**Salida esperada:**
```
RangeIndex(start=0, stop=7, step=1)
```

## Establecer una columna como índice

```python
bands_ind = bands.set_index("nombre")
print(bands_ind)
```
**Salida esperada:**
```
                     género color_icónico  álbumes_publicados  años_activos
nombre                                                                    
Metallica       Heavy Metal         Negro                  11            40
Queen         Rock Clásico         Blanco                  15            50
Nirvana            Grunge         Negro                   3             7
The Beatles   Rock Clásico         Blanco                  12            10
Pink Floyd   Rock Progresivo         Negro                  15            30
AC/DC          Hard Rock         Negro                  17            50
Led Zeppelin  Rock Clásico         Negro                   9            12
```

## Eliminar un índice

```python
bands_ind.reset_index()
```
**Salida esperada:**
```
         nombre         género color_icónico  álbumes_publicados  años_activos
0    Metallica    Heavy Metal         Negro                  11            40
1       Queen  Rock Clásico         Blanco                  15            50
2     Nirvana        Grunge         Negro                   3             7
3  The Beatles  Rock Clásico         Blanco                  12            10
4  Pink Floyd  Rock Progresivo         Negro                  15            30
5       AC/DC     Hard Rock         Negro                  17            50
6  Led Zeppelin  Rock Clásico         Negro                   9            12
```

## Los índices facilitan el subconjunto

```python
bands[bands["nombre"].isin(["Metallica", "Nirvana"])]
```
**Salida esperada:**
```
      nombre     género color_icónico  álbumes_publicados  años_activos
0  Metallica  Heavy Metal         Negro                  11            40
2   Nirvana      Grunge         Negro                   3             7
```

## Uso de `.pivot_table`

```python
bands_pivot = bands.pivot_table("álbumes_publicados", index="género", columns="color_icónico")
print(bands_pivot)
```
**Salida esperada:**
```
color_icónico    Blanco  Negro
género                       
Grunge             NaN    3.0
Hard Rock          NaN   17.0
Heavy Metal        NaN   11.0
Rock Clásico      13.5    9.0
Rock Progresivo    NaN   15.0
```

---

¡Ahora intenta estos ejemplos en tu entorno de Pandas!


[`Ejemplo`](./code/1.3-slicing_data.ipynb)