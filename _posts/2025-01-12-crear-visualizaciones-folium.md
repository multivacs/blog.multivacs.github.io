---
title: Cómo crear visualizaciones de mapas en Python con Folium
description: Genera mapas interactivos personalizados con la librería Folium.
author: mario
date: 2025-01-12 22:30:00 +0100
categories: [Tecnología y Programación, Visualización]
tags: [introducción, empezar, data science]
pin: false
math: false
mermaid: false
image:
  path: assets/img/posts/2025-01-12-crear-visualizaciones-folium/miniatura.png
  alt: Visualizaciones con Folium.
---


- [1. Introducción](#1-introducción)
- [2. Requisitos previos](#2-requisitos-previos)
- [3. Crear un mapa básico](#3-crear-un-mapa-básico)
- [4. Leer y añadir información desde un archivo GeoJson](#4-leer-y-añadir-información-desde-un-archivo-geojson)
- [5. Añadir marcadores simples](#5-añadir-marcadores-simples)
- [6. Agrupar marcadores en un clúster](#6-agrupar-marcadores-en-un-clúster)
- [7. Crear un mapa de calor](#7-crear-un-mapa-de-calor)
- [Ejemplo interactivo](#ejemplo-interactivo)



## 1. Introducción

Folium es una librería de Python que te permite crear mapas interactivos de manera sencilla. En este post veremos:
1. Cómo crear un mapa básico
2. Leer un archivo GeoJson y mostrarlo en el mapa
3. Añadir marcadores simples, clústers y mapas de calor


## 2. Requisitos previos

Antes de empezar, deberás instalar Folium si no lo tienes aún:

```bash
pip install folium
```

O si cuentas con un entorno de conda, que es lo que recomiendo, puedes instalarlo con:
```bash
conda install folium
```

Sobre cómo instalar un entorno de desarrollo con `conda` y cómo configurarlo, podéis utilizar el siguiente tutorial donde se explica paso por paso: [How to Install Conda in VSCode](https://www.youtube.com/watch?v=eN6PCC_RoVI)


## 3. Crear un mapa básico

Primero, para crear un mapa deberemos de importar la librería e indicarle una posición inicial en coordenadas ([latitud, longitud]) y si queremos podemos ajustar un zoom inicial.  
Luego podremos movernos sobre el mapa, pero por ahora, pongamos que queremos centrar el mapa en la ciudad de Madrid:

```python
import folium

# Creamos el mapa centrado en Madrid
m = folium.Map(location=[40.428, -3.76], zoom_start=12)

# Mostramos el mapa
m
```

## 4. Leer y añadir información desde un archivo GeoJson

Vamos a añadir información relativa a los distritos de Madrid. Este método es útil cuando queremos representar fronteras en nuestro mapa, o dividirlo por secciones.

Para el ejemplo, utilizaremos el siguiente archivo GeoJson que podréis encontrar en la web [The Metabolism of Cities](https://data.metabolismofcities.org/library/maps/35568/view/)

Para posteriormente poder añadir más información, en vez de añadirlos directamente sobre el mapa, lo que haremos será crear una capa GeoJson, que posteriormente aparecerá en el lado derecho superior del mapa, y que nos permitirá ocultar o mostrar la información de los distritos.

```python
import json

# Leemos el archivo GeoJson
with open('neighbourhoods.geojson', 'r') as file:
    distritos = json.load(file)

# Crear el mapa centrado en Madrid
m = folium.Map([40.428, -3.76], zoom_start=12)


# Añadir los distritos como una capa GeoJson
distritos_layer = folium.FeatureGroup(name='Distritos', show=True)

folium.GeoJson(distritos,
               tooltip=folium.GeoJsonTooltip(
                   fields=['neighbourhood'],
                   aliases=['Barrio:'],
                   localize=True
               )
            ).add_to(distritos_layer)

# Agregar la capa al mapa
distritos_layer.add_to(m)

# Añadir el control de capas para activar/desactivar los distritos
folium.LayerControl().add_to(m)

# Mostrar el mapa
m

```

![](assets/img/posts/2025-01-12-crear-visualizaciones-folium/map1.png)
_Mapa de Madrid con distritos_


## 5. Añadir marcadores simples

Ahora vamos a añadir marcadores individuales en el mapa.

```python
# Añadir un marcador en una ubicación
folium.Marker(
  location=[40.4169019, -3.7034834],
  popup='Plaza del Sol'
).add_to(m)
```

![](assets/img/posts/2025-01-12-crear-visualizaciones-folium/map2_marker.png)
_Marker simple_


## 6. Agrupar marcadores en un clúster

Si necesitas mostrar la información de varios marcadores, la mejor manera de hacerlo es utilizando `folium.plugins.MarkerCluster`.  
Esta función agrupará automáticamente los marcadores según la distancia, y conforme nos acerquemos en el mapa irán apareciendo los marcadores individuales.

```python
from folium.plugins import MarkerCluster
import pandas as pd


df = pd.DataFrame({
    'latitude': [40.417, 40.428, 40.430],
    'longitude': [-3.703, -3.76, -3.74],
    'neighbourhood': ['Centro', 'Salamanca', 'Retiro']
})

locations = list(zip(df.latitude, df.longitude))
cluster = MarkerCluster(locations=locations, popups=df["neighbourhood"].tolist())

m.add_child(cluster)
```

![](assets/img/posts/2025-01-12-crear-visualizaciones-folium/map3_cluster.png)
_Mapa de clústers_


## 7. Crear un mapa de calor

Cuando necesitamos mostrar información de densidades, o queremos mostrar información adicional en el mapa, podemos utilizar un mapa de calor con `folium.plugins.HeatMap`.

```python
from folium.plugins import HeatMap

heat_data = list(zip(df.latitude, df.longitude))

HeatMap(heat_data).add_to(m)
```

![](assets/img/posts/2025-01-12-crear-visualizaciones-folium/map4_heatmap.png)
_Mapa de calor_



## Ejemplo interactivo

En este mapa de ejemplo hemos creado un mapa de la ciudad de Madrid, indicando mediante clústers de marcadores los alojamientos y restaurantes, y añadiendo mediante un pequeño popup información de horarios o teléfono.

Los datos se han obtenido directamente de la web de 'datos.gob.es', en:
- [Alojamientos](https://datos.gob.es/en/catalogo/l01280796-alojamientos-de-la-ciudad-de-madrid-www-esmadrid-com)
- [Restaurantes](https://datos.gob.es/en/catalogo/l01280796-restaurantes-con-perfil-turistico-de-la-ciudad-de-madrid-www-esmadrid-com)

Dado que los datos se encuentran en XML, deberemos de parsearlos y transformarlos en dataframes.  
El código podéis encontrarlo en [GitHub](https://github.com/multivacs/madrid-map-restauracion).


<iframe 
  src="\assets\img\posts\2025-01-12-crear-visualizaciones-folium\mapa_interactivo.html" 
  width="100%" 
  height="600px" 
  frameborder="0" 
  allowfullscreen>
</iframe>