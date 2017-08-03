## PostGIS ♥ Protobuf

---

### Introduction

* Björn Harrtell, Sweden
* Septima, Denmark

Note:
At Septima I work as a geospatial developer.

---

### Subject

* Encoding Protobuf formats in PostGIS
* Mapbox Vector Tiles (lossy)
* Bonus: Geobuf (lossless)

Note:
This talk is about a upcomming feature in PostGIS 2.4 to support outputting data in two Protobuf based formats.

Protobuf is a binary encoding specification from Google for structured data. Simplified I think it can perhaps be seen as a binary equivalent of XML.

---

### Why encode vector tiles in PostGIS?

* Custom projections
* Simplify toolchain
* Reduce I/O for potential performance wins

Note:
A few years back I had an assigment to build a mobile client with offline support and the ability to download and handle many layers of vector data for which vector tiles seemed the best available choice because it's optimized for rendering and size. A requirement was to use a swedish reference system.

So my main reason to look into encoding vector tiles was that existing toolchains only supported spherical mercator and was relatively complex.

I did hack my own toolchain in Java at one point and while it worked I wasn't happy to maintain it.

Middleware requires I/O and (de)serialization.

So I thought why not do this directly in PostGIS.

---

### Two new functions

* <a target="_blank" href="https://postgis.net/docs/manual-dev/ST_AsMVTGeom.html">ST_AsMVTGeom</a>
* <a target="_blank" href="https://postgis.net/docs/manual-dev/ST_AsMVT.html">ST_AsMVT</a>

Note:
At first I only had ST_AsMVT but at some point a Mapbox developer Blake Thompson informed me that
the MVT specification require geometry to be OGC valid and in a specific orientation. Even if your
input geometry is valid it can become invalid when converted to the local coordinate space of a vector tile.

* Show the docs, show the vector tile specification

ST_AsMVTGeom is used to transform a geometry into tile coordinate space.

ST_AsMVT is an aggregate function to encode a set of rows with transformed geometry + attributes into the binary vector tiles format.

The initial version of ST_AsMVT took a SQL string as input and queried it internally. It was Paul's suggestion to make it an aggregate function which required some deep diving into PostgreSQL internals.

So I reworked the implementation into these two functions to make it explicit that there is a geometry transformation step
which is most likely also the most computation intensive step because it includes checking and correcting geometry validity.

Mapbox has their own library https://github.com/mapbox/wagyu to support the needed geometry transformation. It would be interesting to integrate into PostGIS but not trivial as it's written in a modern variant of C++.

---

### Bonus function

* <a target="_blank" href="https://postgis.net/docs/manual-dev/ST_AsGeobuf.html">ST_AsGeobuf</a>
* Similar to GeoJSON but more compact

Note:
I've also implemented ST_AsGeobuf, which I actually did before vector tiles because while also based on protobuf it's a more simple encoding so was a good start for me.

Can be a useful alternative to GeoJSON when you need larger volumes of data on the client side. Can complement vector tiles for when you need get the lossless source data.

---

### Demonstration

* Basic usage

Note:
* Show sample data (EPSG:3857) in QGIS.
* Show a simple as possible script to produce four tiles.
* Show the tiles with a simple OpenLayers viewer.

---

### mvtile.sql

```sql
SELECT ST_AsMVT('land', 512, 'geom', q)
FROM (SELECT
  id,
  ST_AsMVTGeom(
    geometry, 
    ST_MakeEnvelope(:xmin,:ymin,:xmax,:ymax,3857),
    512, 0, true
  ) AS geom
FROM foss4g.ne_50m_land_3857
WHERE
  geometry && ST_MakeEnvelope(:xmin,:ymin,:xmax,:ymax,3857)
) as q WHERE geom IS NOT NULL
```

### psql

```sh
psql -At \
  -v xmin=-20037508.342789244 \
  -v ymin=0 \
  -v xmax=0 \
  -v ymax=20037508.342789244 \
  -f mvtile.sql | xxd -r -p >./1/0/0.pbf
```

Note:
SQL is a backwards language to lets begin from the bottom.

We're requiring that geometry is not null, which can happen due to small geometries collapsing because they are smaller than a tile coordinate pixel.

Then we filter on a bbox which should be the geometric bounds of the tile. If we where to use a tile buffer (to fix boundary render bugs) we would need to add that too here.

Then we specify the source table foss4g.ne_50m_land_3857 and run its geometries through ST_AsMVTGeom. ST_AsMVTGeom also needs the geometric bounds of the tile but should not include any buffer. 512 is the resolution of the tile, 0 buffer and true to have it clip the geometries.

I then run the result through ST_AsMVT.

Now I can use mvtile.sql with psql to query for the first quadrant tile of the world.

Note that psql does not output raw binary, it's in hex encoded format so I use the xxd command to decode it to raw binary.

* Show tile in OpenLayers
* Generate rest of the tiles and show
* Switch styling

---

### PostgreSQL COPY

* Does not output raw binary
* *"The binary file format consists of a file header, zero or more tuples containing the row data, and a file trailer. Headers and data are in network byte order."*

Note:
One might wonder if/why I'm not using the PostgreSQL COPY command. It's because it does not output raw binary.

If there was an option to output raw binary I would not need the script that was demonstrated previously, I could simply output the tiles directly from PL/pgSQL. Perhaps an opportunity for a future contribution?

The current optimal way to use ST_AsMVT is through a PostgreSQL driver where you can read the binary directly.

---

### How?

* <a target="_blank" href="https://github.com/protobuf-c/protobuf-c">protobuf-c</a>
* <a target="_blank" href="https://github.com/mapbox/vector-tile-spec/tree/master/2.1">vector-tile-spec</a>
* Pitch the idea and a POC on the postgis-devel list to get interest
* Talk Paul Ramsey out of having to make the code unit testable
* Get sponsoring from Carto
* Regression tests

Note:
Arguments against unit testable code was probably pretty weak but at least Paul
did not say it was unacceptable. :)

---

### Future development

* Use https://github.com/mapbox/wagyu in PostGIS
* Encourage use of ST_AsMVT in tile servers like t-rex

---

### End!

![Image](./assets/md/assets/twitter.png)