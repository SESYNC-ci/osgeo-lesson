---
---

## Geometry Engine Open Source (GEOS)

GEOS works on vectors, also known as geometric objects, and adds advanced GIS functionalities (topological operations) to complement the essential reading, writing and translating utilities in GDAL.

Like GDAL, GEOS is primarily intended to be a library used by other software.
Unlike GDAL, GEOS does not provide its own collection of command line utilities (like `gdalinfo`).

<!--split-->

One piece of software using GEOS is PostgreSQL with the PostGIS extension.

Log back into <http://pgstudio.research.sesync.org>

![]({{ site.baseurl }}/images/pgstudio-login.png)

<!--split-->

In the SQL window we can execute PostGIS functions that rely on the GEOS libary.
A simple example is the function `ST_Length`, where ST indicates the function accepts spatial types as arguments.

~~~
SELECT ST_Length(ST_GeomFromText('LINESTRING(0 0, 1 1)'));
~~~
{:.input}

~~~
    st_length
-----------------
1.4142135623731
(1 row)
~~~
{:.output}

<!--split-->

A very common vector operation in spatial analysis is to create a buffer around a spatial object.

~~~
SELECT ST_AsText(ST_Buffer(ST_GeomFromText('POINT(0 0)'), 1, 1));
~~~
{:.input}

~~~
    st_astext_
----------------
POLYGON((1 0, 0 -1, -1 0, 0 1, 1 0))
~~~
{:.output}

Exercise
: Calculate an approximation to Pi, the ratio of a circle's circumference to its diamter,  using GEOS functionality built into PostGIS. The function `ST_Perimeter` gives you the length of the perimiter of a polygon.

<!--split-->

Naturally, this is all more interesting with actual data.

~~~
SELECT id, ST_AsText(ST_Transform(restaurants.geom, 4326))
FROM ch01.restaurants
JOIN ch01.highways
ON ST_Intersects(
    ST_Buffer(restaurants.geom, 100), highways.geom)
WHERE feature like '%Toll Road';
~~~
{:.input}

~~~
 id   |        st_astext
------+-------------------------
22310 | POINT(-75.2094 40.6943)
25011 | POINT(-121.499 45.7115)
(2 rows)
~~~
{:.output}

Question
: Has anybody actually got an answer? Thirty simultaneous spatial queries might be a bit much for our toy server.
