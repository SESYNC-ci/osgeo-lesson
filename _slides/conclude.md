---
---

## Summary

The open source stack has two essential libraries at the bottom: GDAL of reading, writing and translating raster and vector data, and GEOS for geometric calculations on vector data.

We will move up the stack to software interacting with these libraries in the next lesson, but the command line utilities offered by GDAL are available for batch processing of spatial data using a shell script.

Projections distort the world - be aware of the spatial reference system your spatial data employ. If possible, find spatial data in an appropriate PCS for your analysis or convert unprojected data with a known GCS to an appropriate PCS.
