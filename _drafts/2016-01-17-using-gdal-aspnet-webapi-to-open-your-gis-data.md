---
layout: post
title:  "Using GDAL and ASP.NET Web API to open your GIS data"
date:   2016-01-24 21:36:00
categories: blog
---

In this adventure, we'll build together a REST API with
[ASP.NET Web API](http://www.asp.net/web-api) and
[GDAL ogr2ogr](http://www.gdal.org/ogr2ogr.html) to liberate
your data in many formats without too much coding.  This follows a
[previous post]({% post_url 2016-01-17-leveraging-opensource-to-do-opendata-seamlessly %})
highlighting things to consider before rolling your own solution in this space.

What I seek to achieve:

- An api fun to use and easy to work with, no matter the language and environment used
  (C#, PL/SQL, powershell, curl, etc.)
- The ability to rename fields or specialize them depending on the formats
- Supports for open formats:
  - [GeoJSON](http://geojson.org/) for the general web
  - [GML](http://www.opengeospatial.org/standards/gml) for the ministries
  - CSV+[WKT](http://www.opengeospatial.org/standards/wkt-crs) for open-data enthusiasts
- Supports for popular proprietary formats:
  - [KML](https://developers.google.com/kml/documentation/kmlreference), KMZ (KML compressed)
  - ESRI Shapefile (multi-file format) ([pdf spec](https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf))
- Supports for projections by EPSG codes to expose datasets in geographic
  or projected coordinate systems

Why I chose ASP.NET versus other frameworks ?

Making web apis can be done in almost any language: php, js, ruby, python, java, etc.
We corporatively chose ASP.NET for this project simply because:

- We are mostly a C# shop when we hack stuff
- ASP.NET Web API is heavily used at [my] work. It's better to have wide internal support
  than bleeding edge in another technology stack.

*[GML]: Geography Markup Language
*[CSV]: Comma Separated Values
*[WKT]: Well Known Text
*[EPSG]: European Petroleum Survey Group
*[KML]: Keyhole Markup Language