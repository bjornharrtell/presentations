## PostGIS ♥ Protobuf

---

### Introduction

* Björn Harrtell, Sweden
* Septima, Denmark

Note:
At Septima I work as a geospatial developer.

---

### Subject

* Encoding Mapbox Vector Tiles in PostGIS
* Bonus: Encoding Geobuf in PostGIS
* Both formats derive from Google Protobuf

Note:
Especially vector tiles has seen a rise in popularity.

---

### Alternative subject

* How a JavaScript developer convinced the PostGIS PSC to accept his C code

---

### Why encode vector tiles in PostGIS?

* Custom projections
* Simplify toolchain
* Reduce I/O for potential performance wins

Note:
Main reason was that existing toolchains only supported spherical mercator.
Middleware requires I/O and (de)serialization.
So I thought why not do it as a PostGIS function.

---

### Two new functions

* [ST_AsMVTGeom](https://postgis.net/docs/manual-dev/ST_AsMVTGeom.html)
* [ST_AsMVT](https://postgis.net/docs/manual-dev/ST_AsMVT.html)

Note:
At first I had only ST_AsMVT but at some point a Mapbox developer Blake Thompson informed me that
the MVT specification require geometry to be OGC valid and in a specific orientation. So I reworked the
implementation into these two functions to make it explicit that there is a geometry transformation step
which is most likely also the most computation intensive step because it includes checking and correcting geometry validity.

Mapbox has their own library https://github.com/mapbox/wagyu to support the needed geometry transformation which would be interesting to integrate into PostGIS but not trivial as it's written in a modern variant of C++.

---

### Demonstration

* ...

Note:
* Show sample data (EPSG:3857) in QGIS.
* Show a simple as possible script to produce four tiles.
* Show the tiles with a simple OpenLayers viewer.

---

### PostgreSQL COPY

* Does not output raw binary
* *"The binary file format consists of a file header, zero or more tuples containing the row data, and a file trailer. Headers and data are in network byte order."*

Note:
If there was an option to output raw binary I would not need the script that was demonstrated previously, I could simply output the tiles directly from PL/pgSQL. Perhaps an opportunity for a future contribution?

---

### How?

* [protobuf-c](https://github.com/protobuf-c/protobuf-c)
* [vector-tile-spec](https://github.com/mapbox/vector-tile-spec/tree/master/2.1)
* Pitch the idea and a POC on the postgis-devel list to get interest
* Talk Paul Ramsey out of having to make the code unit testable
* Get sponsoring from Carto

Note:
Arguments against unit testable code was probably pretty weak but at least Paul
did not say it was unacceptable. :)

### Additional how

* Don't mention I'm really mostly a JavaScript developer
* Regression tests
* Code is small and tidy
* Millions of tiles has been created

Note:
Might explain why I couldn't make the code unit testable and got into some troubles
during the implementation.

---

### Custom projections

* Normally vector tiles are in the projection to rule us all (Spherical Mercator)
* What about real world applications using local projections and OpenLayers?
* ST_AsMVT works with any projection as it does not assume a tiling scheme

---

### Demonstration

* ...

Note:
Show GeoDanmark data on an ortho in EPSG:25832

---

### End!

![Logo](assets/images/twitter.png) [@bjornharrtell](https://twitter.com/bjornharrtell)