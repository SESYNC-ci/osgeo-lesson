---
---

## Geographic Coordinate Systems (GCS)

A geographic coordinate system (GCS) is a reference system that makes it possible to specify locations on the surface of the earth by a latitude and longitude.

An angular unit of measure
: The angular unit of measure is usually a degree, or one 360th of a circle, and fractional degrees are usually specified as decimals.
  
A prime meridian
: The location of 0° longitude, e.g. the Royal Observatory, Greenwich, UK

A datum
: An apprimation to the shape of the earth's surface **and** where (in the GCS being defined) certain fixed positions are located. A spheroid (a flattish sphere) is used to approximate this shape, and the reference positions anchor its surface to known points.

===

### Spheroids and Geoids

- Set an elipse on edge like a coin and spin it: the three dimensional shape you see is a spheroid. This is a simple geometric object.

- A surface defined by the Earth's gravity field is called the geoid. The shape of the geoid is irregular, but overall, it approximates mean sea level (or where mean sea level would be without the continents).

- The geoid is related to a spheroid by it's height, which can be either positive or negative, on a straight line perpendicular to the spheroid. Note that this height is not the height of the ground, or elevation.

===

### Spheroids and Geoids

![]({{ site.baseurl }}/images/spheroid.png)

<aside class="notes">
Although highly exaggerated, this graphic illustrates that the earth itself (the black line) is irregularly shaped. The blue spheroid works well in two areas, but not over the entire surface of the earth. The red spheroid works well in only one area, but it may be a better fit there than the blue spheroid. With the advent of global positioning systems (GPS), new datums and ellipsoids have been developed for the entire globe. 

Spheroids create a totally smooth surface across the world, but because this does not reflect reality very well, this ability of a local datum to incorporate local variations in elevation is important.
</aside>

===

### Datum

Every geographic coordinate system begins with a precisely surveyed starting point.

- Provides a frame of reference for measuring relative position
- Defines the origin and orientation for lines of latitude and longitude
- Datum transformations
- e.g. 'WGS84'

Question:
: Examine the output of gdalinfo for `natural-earth.tif` again (see reminder below). What is the name of Geographic Coordinate System (GEOGCS)? What about the name of the spheroid? Are these different?

~~~
gdalinfo natural-earth.tif
~~~
{:.input}
