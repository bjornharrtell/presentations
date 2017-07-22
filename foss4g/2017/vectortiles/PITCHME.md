## PostGIS + Vector Tiles

---

### Introduction

* Björn Harrtell
* Septima P/S

---

### Subject

* Encoding MapBox Vector Tiles with PostGIS inside the database

---

### Alternative subject

* How a JavaScript developer convinced the PostGIS PSC to accept his C code

---

### Why encode MVT in PostGIS?

* Reduce I/O for potential performance wins
* Simplify toolchain

---

### Two new functions

* [ST_AsMVTGeom](https://postgis.net/docs/manual-dev/ST_AsMVTGeom.html)
* [ST_AsMVT](https://postgis.net/docs/manual-dev/ST_AsMVT.html)

Note:
At first I had only ST_AsMVT but at some point MapBox developer Blake Thompson informed me that
the MVT specification require geometry to be OGC valid and in a specific orientation. So I reworked the
implementation into these two functions to make it explicit that there is a geometry transformation step
which is most likely also the most computation intensive step because it includes checking and correcting geometry validity.

MapBox has their own library https://github.com/mapbox/wagyu to support the needed geometry transformation which would be interesting to integrate into PostGIS but not trivial as it's written in a modern variant of C++.

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
* Talk Paul Ramsey out of having to make the code cunit testable
* Get sponsoring from CartoDB
* Don't mention I'm really a JavaScript developer

---

### Custom projections

* Normally vector tiles are in the projection to rule us all (Spherical Mercator)
* What about real world applications using local projections and OpenLayers?
* ST_AsMVT works with any projection as it does not assume a tiling scheme

---

### Demonstration

* ...

Show GeoDanmark data on an ortho in EPSG:25832