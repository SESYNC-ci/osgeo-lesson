---
---

## Projected Coordinate Systems (PCS)

- A projected coordinate system (PCS) is defined on a flat, two-dimensional surface.
- Unlike a geographic coordinate system, a projected coordinate system has constant lengths, angles, and areas across the two dimensions. 
- If you allow height above the flat surface, then you can locate any point in three dimensions with x, y, and z coordinates (these are not coordinates in Space!)

<!--split-->

A projected coordinate system is defined by four components:

- a geographic coordinate system
- a map projection
- any parameters needed by the map projection
- a linear unit of measure (such as feet or meters)

Question
: What GCS is used in `westernfires_vir_2015231_geo.tif`? What is the map projection?

<!--split-->

### Why use a projected coordinate system?

- Lat/lon is good system for storing spatial data, but areas and distances must be explicitly calculated on a curved surface.
  
- You are making a map in which you want to preserve one or more of these properties: area, shape, distance, and direction.

- You are making a small-scale map such as a national or world map. With a small-scale map, your choice of map projection determines the overall appearance of the map. For example, with some projections, lines of latitude and longitude will appear curved; with others, they will appear straight.

<!--split-->

### Map Projections

Converts the earth's three-dimensional surface to a map's two-dimensional surface. This mathematical transformation is commonly referred to as a map projection. 

![]({{ site.baseurl }}/images/orange.png){:width="45%"}
![]({{ site.baseurl }}/images/projections.png){:width="45%"}
{:.vertical-align}

<!--split-->

Using GDALs ability to re-project raster images with `gdalwarp`, let's compare two rasters.

~~~
gdalsrsinfo -o wkt urban-areas.tif > urban-area.prj
~~~
{:.input}

~~~
gdalwarp -t_srs urban-areas.prj westernfires_vir_2015231_geo.tif westernfires_vir_2015231_geo-prj.tif
gdalinfo westernfires_vir_2015231_geo-prj.tif
~~~
{:.input}

~~~
gdal_translate -projwin -139.2611826 57.8698551 -80.7311826 22.2398551 urban-areas.tif urban-areas-west.tif
~~~
{:.input}
