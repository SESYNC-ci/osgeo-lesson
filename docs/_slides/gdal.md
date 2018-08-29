---
---

### Geospatial Data Abstraction Library (GDAL)

GDAL interprets between a vast collection of storage formats and applications that read or write spatial data. It has a single abstract data model for rasters, and another for vector data. Because GDAL knows all about different formats, it includes many tools for translating and processing geographical data.

~~~
gdalinfo --formats
~~~
{:.input}
~~~
Supported Formats:
  VRT (rw+v): Virtual Raster
  GTiff (rw+vs): GeoTIFF
  NITF (rw+vs): National Imagery Transmission Format
  ...
~~~
{:.output}

===

For historical reasons `gdal*` commands work with rasters, and `ogr*` commands work with vectors.

~~~
ogrinfo --formats
~~~
{:.input}
~~~

Supported Formats:
  -> "ESRI Shapefile" (read/write)
  -> "MapInfo File" (read/write)
  -> "UK .NTF" (readonly)
  ...
~~~
{:.output}

===

### Looking at Metadata (Rasters)

~~~
cd %sandbox%
cd data
gdalinfo natural-earth.tif
~~~
{:.input}

[//]: # " http://www.naturalearthdata.com/downloads/10m-natural-earth-1/10m-natural-earth/ "
[//]: # " processed with: "
[//]: # " gdal_translate -outsize 50% 50% -co 'COMPRESS=LZW' -co 'TILED=YES' NE1_LR_LC.tif natural-earth.tif "

~~~
Driver: GTiff/GeoTIFF
Files: natural-earth.tif
Size is 8100, 4050
Coordinate System is:
GEOGCS["WGS 84",
  DATUM["WGS_1984",
    SPHEROID["WGS 84",6378137,298.257223563,
      AUTHORITY["EPSG","7030"]],
    AUTHORITY["EPSG","6326"]],
  PRIMEM["Greenwich",0],
  UNIT["degree",0.0174532925199433],
    AUTHORITY["EPSG","4326"]]
Origin = (-180.000000000000000,90.000000000000000)
Pixel Size = (0.044444444444440,-0.044444444444440)
Metadata:
  AREA_OR_POINT=Area
  TIFFTAG_DATETIME=2014:10:18 11:51:41
  TIFFTAG_RESOLUTIONUNIT=2 (pixels/inch)
  TIFFTAG_SOFTWARE=Adobe Photoshop CC 2014 (Macintosh)
  TIFFTAG_XRESOLUTION=72
  TIFFTAG_YRESOLUTION=72
Image Structure Metadata:
  COMPRESSION=LZW
  INTERLEAVE=PIXEL
Corner Coordinates:
Upper Left  (-180.0000000,  90.0000000) (180d 0' 0.00"W, 90d 0' 0.00"N)
Lower Left  (-180.0000000, -90.0000000) (180d 0' 0.00"W, 90d 0' 0.00"S)
Upper Right ( 180.0000000,  90.0000000) (180d 0' 0.00"E, 90d 0' 0.00"N)
Lower Right ( 180.0000000, -90.0000000) (180d 0' 0.00"E, 90d 0' 0.00"S)
Center      (  -0.0000000,   0.0000000) (  0d 0' 0.00"W,  0d 0' 0.00"N)
Band 1 Block=256x256 Type=Byte, ColorInterp=Red
Band 2 Block=256x256 Type=Byte, ColorInterp=Green
Band 3 Block=256x256 Type=Byte, ColorInterp=Blue															
~~~
{:.output}

===

### Looking at Metadata (Vectors)

~~~
ogrinfo -ro -so ne_10m_urban_areas
~~~
{:.input}

~~~
INFO: Open of `ne_10m_urban_areas'
  using driver `ESRI Shapefile' successful.
1: ne_10m_urban_areas (Polygon)
~~~
{:.output}

~~~
ogrinfo -ro -so ne_10m_urban_areas ne_10m_urban_areas
~~~
{:.input}

~~~
INFO: Open of `ne_10m_urban_areas'
using driver `ESRI Shapefile' successful.
	  
Layer name: ne_10m_urban_areas
Geometry: Polygon
Feature Count: 11878
Extent: (-157.991183, -51.053037) - (178.033834, 69.769855)
Layer SRS WKT:
GEOGCS["GCS_WGS_1984",
  DATUM["WGS_1984",
    SPHEROID["WGS_84",6378137.0,298.257223563]],
  PRIMEM["Greenwich",0.0],
  UNIT["Degree",0.017453292519943295]]
scalerank: Integer (10.0)
featurecla: String (50.0)
area_sqkm: Real (13.3)
~~~
{:.output}

===

### Translation

In addition to reading spatial data in all those formats, GDAL provides capabilities for writing data in new formats.
Translations can also occur between the same format with a step that modifies the data or metadata.

Write metadata about a raster object that is missing from the `world.png` raster.

~~~
gdal_translate -a_srs WGS84 -a_ullr -180 90 180 -90 world.png geoworld.tif
~~~
{:.input}

Question
: Compare the output of `gdalinfo` for the original `world.png` and new `geoworld.tif` raster files. What did the "corner coordinates" property of the PNG file correspond to before translation? And after translation?

===

The spatial data processing tools provided by GDAL are executed by giving "arguments" to the gdal_translate, which take the form `-flag param1 param2 ...`, which is how most command line utilities work.

The flag `-outsize` takes two parameters for the horizontal and vertical output size (optionally as percentages of the input size) in pixels.

~~~
gdal_translate -outsize 10% 10% geoworld.tif geoworld-small.tif
~~~
{:.input}

===

The flag `-projwin` takes four parameters that specify the new corners of the output file, giving a subwindow of the input file.

~~~
gdal_translate -projwin -180 90 0 0 geoworld.tif geonw.tif
~~~
{:.input}

Exercise
: Choose coordinates that bound your home state or country, and create a new file called `natural-earth-home.tif` that only includes that area of the `natural-earth.tif`. The order of parameters is upper left "x", upper left "y", lower right "x", lower right "y".

Question
: Why bother with this approach over cropping the image with an image editor?

===

### Conversion

Here's a handy little utility. Ever want to quickly peek at a shapefile? Why not convert it to a raster at the command line?

~~~
gdal_rasterize -ot Byte -burn 255 -tr 0.01 0.01 -l ne_10m_urban_areas ne_10m_urban_areas urban-areas.tif
~~~
{:.input}

Exercise
: Examin the metadata of `urban-areas.tif` using the `-stats` flag. This provides additional information, but does it look right? `gdal_rasterize` is very literal, it set polygons to 255 and everything else to 0, whereas areas outside the polygons might be more appropriately set to "Null". [Read the docs](http://www.gdal.org/gdalinfo.html) to decide how it can be done. Try to re-create the raster so that the mean value is 255.
