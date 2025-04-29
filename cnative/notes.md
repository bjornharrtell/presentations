Hi and welcome to a lightning talk about FlatGeobuf

My name is Björn, I'm a swedish programmer and have been into spatial stuff for a long time. A few years ago I created FlatGeobuf.

So what is FlatGeobuf?

It is a fast binary format for spatial data and attributes.

And it's lossless with similar flexibility as GeoJSON.

Initially my idea was to make a format similar to the shapefile but faster and without the limitations.

---

So why did I make FlatGeobuf?

I think was initially it was due to that I wanted to know how Mapbox Vector Tiles work. As you might know they are based on something called Protobuf, from Google, which think about as kind of XML but for binary.

It was also triggered by that the best format out there for some use cases was still the shapefile.

And then I found a project called flatbuffers, which is also from Google, and it's like Protobuf but faster.

I also found flatbush, a tiny and nice implementation of R-tree spatial index by Volodymyr Agafonkin (who you might know as the creator of Leaflet)

And so, flatbush helped me understand how R-trees works (which is something I had wanted to learn about for some time) and to create a format to beat the shapefile you really need an efficient spatial index to support making spatial filtered queries against the data.

---

And so around September 2018 I made the initial commits to implement what became FlatGeobuf.

It went through iterations also at spec level and finally in January 2020 I was happy enough with it to consider it more or less "done".

I implemented support in GDAL which was released as GDAL 3.1 in May 2020, that was an important stepping stone for FlatGeobuf ot make it available for example in QGIS.

FlatGeobuf is also via plugin available in GeoServer as a data source or WFS output format.

--

Ok so I haven't mentioned Cloud-Native at all?

Well, it is because I didn't consider Cloud-Native when I made FlatGeobuf but it turns out FlatGeobuf is pretty much Cloud-Native but perhaps mostly by accident.

A design goal of the final spec was to make the format I/O efficient and support streaming and piping and that is what makes it work well in Cloud-Native.

---

Live demo

---

* Drop in replacement for Shapefile, GeoJSON, GML
* Serialization format for simple features in system to system communication
* Output format from WFS or OGC API


---

## Thanks for listening!
And a special thanks to FlatGeobuf contributors ❤️