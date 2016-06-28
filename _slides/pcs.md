---
---

## Projected Coordinate Systems (PCS)

- A projected coordinate system (PCS) is defined on a flat, two-dimensional surface
- Unlike a geographic coordinate system, a projected coordinate system has constant lengths, angles, and areas across the two dimensions. 
- Locate x, y, and z positions of point, line, and area features in two or three dimensions. 

<!--split-->

- A projected coordinate system is defined by four components:
  - a geographic coordinate system
  - a map projection
  - any parameters needed by the map projection
  - a linear unit of measure (such as feet or meters)
- PCS <- GCS <- Datum <- Spheroid ~ Geoid.

All shapefiles (SHP) come with a PRJ file

<!--split-->

### Why a projected coordinate system?

- Accurate distance measurements 
  - Lat/longitude is good system for storing spatial data, but areas and distances are not constant across the earth
- You are making a map in which you want to preserve one or more of these properties: area, shape, distance, and direction.
- You are making a small-scale map such as a national or world map. With a small-scale map, your choice of map projection determines the overall appearance of the map. For example, with some projections, lines of latitude and longitude will appear curved; with others, they will appear straight.

<aside>
Influence calculations
Influence dimensions
Influence appearance
</aside>

<!--split-->

### Map Projections

Converts the earth's three-dimensional surface to a map's two-dimensional surface. This mathematical transformation is commonly referred to as a map projection. 

|![]({{ site.baseurl }}/images/orange.png)|![]({{ site.baseurl }}/images/projections.png)|

