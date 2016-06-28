---
---

## Geographic Coordinate Systems (GCS)

- Compare Geographic and Project Coordinate Systems
- A geographic coordinate system (GCS) is a reference system that uses a three-dimensional spherical surface to identify points or areas on the surface of the earth. 
  - an angular unit of measure
  - a prime meridian
  - a datum, which includes a spheroid
- The angular unit of measure is usually degrees, in which the unit represents one part in 360 of a circle. 
- The prime meridian defines the zero value for longitude, the equator defines zero value for latitude
- The datum specifies the position of the sphere or spheroid relative to the center of the earth. It defines the origin and orientation of latitude and longitude lines.

<aside>
Lat/Lon is a coordinate system, but not a geographical coordinate system without a specified datum.
</aside>

<!--split-->

### Spheroids

- The surface of the Earth's gravity field is called the geoid. The shape of the geoid is irregular, but overall, it is approximately the same as mean sea level. This is approximated with a spheroid.

- Each spheroid approximates a specific geographic area.

- A datum is built on top of the selected spheroid, and it can incorporate local variations in elevation. 

![][{{ site.baseurl }}/images/spheroid.png]

<aside>
Although highly exaggerated, this graphic illustrates that the earth itself (the black line) is irregularly shaped. The blue spheroid works well in two areas, but not over the entire surface of the earth. The red spheroid works well in only one area, but it may be a better fit there than the blue spheroid. With the advent of global positioning systems (GPS), new datums and ellipsoids have been developed for the entire globe. 

Spheroids create a totally smooth surface across the world, but because this does not reflect reality very well, this ability of a local datum to incorporate local variations in elevation is important.
</aside>

<!--split-->

### Datum

Every map projection and coordinate system begins with a precisely surveyed starting point.

- Provides a frame of reference for measuring relative position
- Defines the origin and orientation of lat/lon lines.
- Datum transformations
- e.g. 'WGS84'

![][{{ site.baseurl }}/images/datum.png]

<aside>
The starting point and the network of points that extends from it is called the datum. 

Although highly exaggerated, this graphic illustrates that the earth itself (the black line) is irregularly shaped. The blue spheroid works well in two areas, but not over the entire surface of the earth. The red spheroid works well in only one area, but it may be a better fit there than the blue spheroid. With the advent of global positioning systems (GPS), new datums and ellipsoids have been developed for the entire globe. WGS 84 is now accepted as a universal global datum.

These examples are two common world spheroids in use today with their values rounded to the nearest meter. For each spheroid, the difference between its major axis and its minor axis is less than 0.34 percent.
</aside>

