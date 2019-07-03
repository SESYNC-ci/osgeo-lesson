---
---

GIS software is designed to capture, manage, analyze, and display (on a map!) all forms of geographically referenced information. Before diving deep into software, we review basic concepts for geographical data and the associated open source tools.

===

## Geographical Data

Breaking down these uses of GIS, we find the usual components of any data driven project. The strong emphais on *geographical* marks the special attention that spatial attributes of data require.

| **capture** | record data with sufficient context to be useful                     |
| **manage**  | work with vast amounts of data, often captured in different contexts |
| **analyze** | rely on the inherent spatial relationships between data              |
| **display** | conveniently display data in its native form (on a map!)             |

===

### So What?

![]({% include asset.html path="images/korea-wrong.png" %})  
*[Source][korea]*

<aside class="notes">
One of the most famous mistakes, amongst academic geographers at least, was an article in the Economist magazine on the threat of missiles from North Korea.
The first map they published, shown above, did not account for the fact that the world is spherical.
It massively underestimated the reach of the North Korean missile designs.
The corrected version is shown below, using the proper interpretation of the same missile-ranges.
</aside>

===

![]({% include asset.html path="images/korea-right.png" %})  
*[Source][korea]*

[korea]: http://spatial.ly/2011/01/geographical-mistakes-keeping-geographers-busy/

===

### Why Open Source

- Pros
  - Reproducible research principle (no proprietary code)
  - Affordable for researchers
  - Ease of licensing
  - Friendly user community
  - Available on multiple platforms (e.g. Windows, Linux, Mac)
- Cons
  - Fewer training resources
  - Less integration (Pro?)

The excellent and canonical alternative is [ESRI's ArcGIS platform](http://www.esri.com/software/arcgis).
