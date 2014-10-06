Fiona-Rasterio-Shapely Cheat Sheet
==================================

Cheat sheet for Fiona/Rasterio/Shapely command-line geodata tools

Vector operations
---

__Get vector information__

	fio info input.shp

__Print vector extent__

	fio info input.shp --bounds

__Print vector coordinate reference system__

	fio info input.shp --crs
	
__Print count of features__

	fio info input.shp --count
	
__List vector drivers__

	TODO

__Convert vectors to GeoJSON__

	fio cat input.shp --dst_crs EPSG:4326 | fio collect --precision 6 > output.json

__Convert between vector formats__

	fio cat input.shp | fio load --driver Shapefile output.shp

__Print count of features with attributes matching a given pattern__

	fio cat input.shp | grep "Search Pattern" -c

__Clip vectors by bounding box__

	TODO

__Clip one vector by another__

	TODO

__Reproject vector:__

	fio cat input.shp --dst_crs EPSG:4326 | fio load --driver Shapefile --dst_crs EPSG:4326 output.shp
	
__Merge features in a vector file by attribute ("dissolve")__

  	TODO

__Merge vector files:__

  	fio cat input1.shp input2.shp | fio load --driver Shapefile merged.shp

__Extract from a vector file based on query__

  	TODO

__Subset & filter all shapefiles in a directory__

  	TODO
