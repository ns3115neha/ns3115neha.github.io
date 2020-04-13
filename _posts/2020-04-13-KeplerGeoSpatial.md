---
published: true
title: Geo Spatial Visualisation Kepler.gl 
categories: [GeoVis]
---


### 4 lines of Pythonic code 

Ever wondered the flexibility of python and Kepler.gl combined how easy it is to visualise Geo Spatial data.


```
import pandas as pd
import keplergl
import geopandas as gpd

read csv data , other formats supported 
data = pd.read_csv("")

convert data into geodataframe
gdf = gpd.GeoDataFrame(data,geometry = gpd.points_from_xy(data.lng,data.lat))

create a base map with kepler
map = keplergl.KeplerGl(height=400,width=800)

add geometry encoded dataframe to map
map.add_data(data = gdf, name = 'dummylayer'
```


![](/images/Kepler/KeplerGL.jpg){: .center-image }

