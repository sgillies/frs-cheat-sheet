Fiona-Rasterio-Shapely Cheat Sheet
==================================

A cheat sheet for Fiona/Rasterio/Shapely command-line geodata tools. Suggestions welcome!

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

Using grep:

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

#### Filter a vector file

Using [jq](http://stedolan.github.io/jq/) and [geojsonio-cli](https://github.com/mapbox/geojsonio-cli). Jq can't
yet handle RS-separated sequences, so use --x-json-seq-no-rs.

	fio cat input.shp --x-json-seq-no-rs \
	| jq 'select(.id=="10")' -c \
	| fio collect \
	| geojsonio

__Subset & filter all shapefiles in a directory__

  	TODO

Raster operations
---
__Get raster information__

	rio info input.tif

__Print raster extent__

	rio info input.tif --bounds

__Print raster coordinate reference system__

	rio info input.tif --crs
	
__Print count of raster bands__

	rio info input.tif --count

__Get raster extent as GeoJSON__

And pipe to geojsonio-cli:

	rio bounds input.tif | geojsonio

__Extract vectors from raster band as GeoJSON__

	rio shapes input.tif --bidx 1 > output.json

__Extract data/nodata vectors from raster as GeoJSON__

	rio shapes input.tif --mask > output.json
	
__Burn vector into raster__

	TODO

(Lots of other operations TODO)
