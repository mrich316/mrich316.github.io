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

Why I chose ASP.NET Web API versus other frameworks ?

Making web apis can be done in almost any language: php, js, ruby, python, java, etc.
We corporatively chose ASP.NET for this project simply because:

- We are mostly a C# shop when we hack stuff
- ASP.NET Web API is heavily used at [my] work. It's better to have wide internal support
  than bleeding edge in another technology stack.

Print the [pdf](http://www.asp.net/media/4071077/aspnet-web-api-poster.pdf) of the http message lifecycle
and keep it close.


Building a custom [MediaTypeFormatter](https://msdn.microsoft.com/en-us/library/system.net.http.formatting.mediatypeformatter%28v=vs.118%29.aspx)
----------------------------------------------------------------------------

**TODO**: EXPLAIN WHAT IS A MEDIATYPEFORMATTER BASED ON THE PDF.

I would like to have an API that takes metadata and binary files at the same time. Being a potential user myself,
the easiest way I know to call such an API would be by doing a ***multipart/form-data*** POST.
Since we want our API to be easy and fun to use, I won't go in other routes that requires extra steps before sending
a file, but here what we could do:

- doing a two-steps approach; calling two endpoints successively: sending the metadata first and the files after **(requires a mediator)**
- sending in bson, protobuf or another wire format **(needs a serializing library)**
- sending binary files in base64 along side metadata in json **(bandwidth unfriendly)**
- POSTing a multipart/form-data containing untouched binary files and text fields for metadata **(good for me!)**


Building a custom [MultipartStreamProvider](https://msdn.microsoft.com/en-us/library/system.net.http.multipartstreamprovider%28v=vs.118%29.aspx) 
-------------------------------------------

**TODO**: EXPLAIN WHAT IS A STREAMPROVIDER

I want my api to be fast and only write on disk when absolutely required by the underlying converters.
We must find a way to handle files in memory when they are small and on disk otherwise.
For that to happen, we must build a custom MultipartStreamProvider.  We can not extend
[MultipartFormDataStreamProvider](https://msdn.microsoft.com/en-us/library/system.net.http.multipartformdatastreamprovider%28v=vs.118%29.aspx)
because this provider always save to disk first. Another requirement: The files need to be
temporary and deleted automatically after the HttpMessageResponse is disposed.
We don't want to program and schedule clean-up tasks (our API must be self-contained)!


Known limitations of current Web API versions
---------------------------------------------

A limitation of current Web API versions: we can not have more than one complex parameter on an ApiController method.
We will have to create a generic type capable of holding binary blobs and simple types at the same time or create
a provider handling this scenario.


*[GML]: Geography Markup Language
*[CSV]: Comma Separated Values
*[WKT]: Well Known Text
*[EPSG]: European Petroleum Survey Group
*[KML]: Keyhole Markup Language