Fiona-Rasterio-Shapely Cheat Sheet
==================================

A cheat sheet for Fiona/Rasterio/Shapely command-line geodata tools. Suggestions welcome!

Vector operations
---

#### Get vector information

	fio info input.shp

#### Print vector extent

	fio info input.shp --bounds

#### Print vector coordinate reference system

	fio info input.shp --crs
	
#### Print count of features

	fio info input.shp --count
	
#### List vector drivers

	TODO

#### Convert vectors to GeoJSON

	fio cat input.shp --dst_crs EPSG:4326 \
	| fio collect --precision 6 > output.json

#### Convert between vector formats

	fio cat input.shp | fio load --driver Shapefile output.shp

#### Print count of features with attributes matching a given pattern

Using grep.

	fio cat input.shp | grep "Search Pattern" -c

#### Clip vectors by bounding box

	TODO

#### Clip one vector by another

	TODO

#### Reproject vector

	fio cat input.shp --dst_crs EPSG:4326 \
	| fio load --driver Shapefile --dst_crs EPSG:4326 output.shp
	
#### Merge features in a vector file by attribute ("dissolve")

  	TODO

#### Merge vector files

  	fio cat input1.shp input2.shp \
  	| fio load --driver Shapefile merged.shp

#### Filter a vector file

Using [jq](http://stedolan.github.io/jq/) for filtering and 
[geojsonio-cli](https://github.com/mapbox/geojsonio-cli) for display of results. Jq can't
yet handle RS-separated sequences, so use --x-json-seq-no-rs.

	fio cat input.shp --x-json-seq-no-rs \
	| jq 'select(.id=="10")' -c \
	| fio collect \
	| geojsonio

#### Filter a vector file in parallel

Using GNU Parallel

	fio cat input.shp --x-json-seq-no-rs \
	| parallel --pipe "jq -c 'select(.id==\"10\")'" \
	| fio collect \
	| geojsonio

#### Subset & filter all shapefiles in a directory

  	TODO

Raster operations
---

#### Get raster information

	rio info input.tif

#### Print raster extent

	rio info input.tif --bounds

#### Print raster coordinate reference system

	rio info input.tif --crs
	
#### Print count of raster bands

	rio info input.tif --count

#### Get raster extent as GeoJSON

And pipe to geojsonio-cli:

	rio bounds input.tif | geojsonio

#### Extract vectors from raster band as GeoJSON

	rio shapes input.tif --bidx 1 > output.json

#### Extract data/nodata vectors from raster as GeoJSON

	rio shapes input.tif --mask > output.json
	
#### Burn vector into raster

	TODO

(Lots of other operations TODO)
