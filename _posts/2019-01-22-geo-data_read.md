---
layout: post
title:  "python读取geos数据"
date:   2019-01-22 18:00:00
categories: Python
tags: Python, geo, geopandas, shapeply
author: LuckyBoy
location: Beijing, China
description: 记录一些python读取geos数据的方法
---
---

# geopandas读取数据

可以使用to_json函数将data_frame数据转为GeoJSON

```python
import geopandas as gpd
data = gpd.read_file("/home/user/data/test_data/point.mif")
json_data = data.to_json()
```

# shaply读取数据

## 1. 读取wkt数据

```python
from shapely import wkt
line = wkt.loads('LINESTRING(104.0812371 30.40341239,104.0811 30.40339,104.08088 30.40336,104.08065 30.40334,104.08052 30.40334,104.0802023 30.40336704)')
```

## 2. 读取GeoJson数据

```python
from shapely import geometry
# 读取geojson
geometry.asShape(json.loads({geojson}))
# 生成GeoJSON
geometry.mapping(shaply_geom)
```