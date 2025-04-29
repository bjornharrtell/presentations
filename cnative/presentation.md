---
marp: true
theme: default
class: invert
---

# FlatGeobuf lightning talk

---

# Who am I?

* Björn Harrtell
* Swedish programmer into spatial stuff
* Created FlatGeobuf

---

# FlatGeobuf - what is it?

* A fast binary (file)format for spatial data and attributes (aka. OGC simple features)
* Lossless
* Similar flexibility in content as GeoJSON
* Similar to the shapefile but faster and without the limitations

---

# FlatGeobuf - why did I make it?

* Born out of curiosity
* I wanted to know how Mapbox Vector Tiles works
  * Protobuf by Google - similar to XML but for binary data
* There was nothing out there that could beat the Shapefile in all use cases
* Found flatbuffers which is like Protobuf but more time efficient
* Found flatbush, a tiny and nice implementation of R-tree spatial index by Volodymyr Agafonkin
* Flatbush helped me understand how R-tree works

---

# FlatGeobuf code history

* Initial commit September 2018
* v3 spec finished January 2020 ("final" spec)
* GDAL driver in 3.1 (May 2020)
 * QGIS
* GeoServer (use as data source or serve as WFS output format)

---

# So I haven't mentioned Cloud-Native?

* Turns out FlatGeobuf is pretty Cloud-Native mostly as an accident
* By v3 I had made the format so that it could be read using few I/O requests and only forward seeks to allow it to be streamed or piped.
* Turns out this helped the Cloud-Native case too

---

# Use cases for FlatGeobuf

* Drop in replacement for Shapefile, GeoJSON, GML
* Serialization format in system to system communication
* Output format from WFS or OGC API

---

# Thanks for listening!
And a special thanks to FlatGeobuf contributors ❤️