---
---

## Distortion

Projected coordinate systems -- they distort the world.

Four spatial properties subject to distortion in PCS:

- shape
- area
- distance
- direction

===

The most recognizable distortion is the result of treating latitude and longitude values as if they were the "x" and "y" values of a projected coordinate system.

![]({% include asset.html path="images/circle.png" %})

===

### Choose Projections Wisely!

| Name        | Feature that is Preserved                              |
|-------------+--------------------------------------------------------|
| Conformal   | Shape                                                  |
| Equal Area  | Area                                                   |
| Equidistant | Distance between one or two foci and every other point |
| Azimuthal   | Direction from one of two points to every other point  |

![]({% include asset.html path="images/preserve.png" %})

===

### Projections that Preserve Shape

Conformal projection: all local angles measured from a point are correct and all local shapes are true. 

Use conformal projection when the map's main purpose involves measuring angles, showing accurate local directions, or representing the shapes of features or contour lines. This category includes:

- Topographic maps and cadastral (land parcel) maps
- Navigation charts 
- Civil engineering maps
- Military maps
- Weather maps

<aside class="notes">
Navigation charts (for plotting course bearings and wind direction)
Weather maps (for showing the local direction in which weather systems are moving)
</aside>

===

### Projections that Preserve Area

Equal-area projection: the size of any area on the map is in true proportion to its size on the earth. You should use equal-area projections to show:

- The density of an attribute with dots (for example, population density)
- The spatial extent of a categorical attribute (for example, land use maps)
- Quantitative attributes by area (for example, gross domestic product by country)

<aside class="notes">
For localized measures, use local UTM: Universal Transverse Mercator is one of the most common nearly-global projected coordinate systems. The system divides the globe into 60 zones every six degrees of longitude. These zones run from pole to pole. Each zone has its own projection parameters to maximize accuracy. East-west measurements are made in meters from an origin local to the specific zone called the central meridian. North-south measurements are made in meters from the equator.
</aside>

===

### How does this impact your spatial analysis?

![]({% include asset.html path="images/blur.png" %})

Unless explicitly calculating geometric attributes on a curved surface, the projection used will affect the result of any such calculations. For a "planar" calculation of the area of the USA, for example, different projections give different results.
