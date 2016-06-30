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

<!--split-->

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

<!--split-->

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

[//]: # " http://www.naturalearthdata.com/http//www.naturalearthdata.com/download/10m/cultural/ne_10m_urban_areas.zip "

<!--split-->

### Translation

- add missing metatdata
- change pixel dimensions
- subset a window

~~~
gdal_translate -a_srs WGS84 -a_ullr -180 90 180 -90 world.png geoworld.tif
~~~
{:.input}

~~~
gdal_translate -outsize 10% 10% geoworld.tif geoworld-small.tif
~~~
{:.input}

~~~
gdal_translate -projwin -180 90 0 0 geoworld.tif geonw.tif
~~~
{:.input}


[//]: # " http://download.osgeo.org/gdal/workshop/world.png "

<!--split-->

### Conversion

~~~
gdal_rasterize -a scalerank -tr 0.1 0.1 -l ne_10m_urban_areas ne_10m_urban_areas/ne_10m_urban_areas.shp urban-areas.tif
~~~
{:.input}

[//]: # " Make this a challenge exercise ... to difference the natural files with a subset of this raster. Tricky part is lining them up. "

