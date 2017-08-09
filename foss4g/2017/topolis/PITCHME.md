## Topolis

---

### Introduction

* Björn Harrtell, Sweden
* Septima, Denmark
* [JSTS](http://bjornharrtell.github.io/jsts)

Note:
At Septima I work as a geospatial developer.
I'm also the author of JSTS, the JavaScript port of Java Topology Suite, used in amongst other things Turf from Mapbox.

---

### Subject

* Topolis JavaScript library
* Can manipulate topological data
* Ported from PostGIS Topology implementation

---

### Typical topological data

* Road networks built from nodes and edges
* Topology is built from simple geometry but with toplogical constraints
* Add the concept face (surface) suitable to represent for example administrative areas

Note:
Some words about what typical topological data is.

Most common is probably road networks build from nodes and edges, like OpenStreetMap.

Topology is built from simple geometry but with toplogical constraints.

Simple geometry is usually defined as individiual points, lines or polygons.

An example of a toplogical contraint is that no edge may overlap another edge.

It's also possible to add the concept face (surface) suitable to represent for example administrative areas.

---

### Prior art

* [ESRI ArcInfo Coverage format](http://desktop.arcgis.com/en/arcmap/10.3/manage-data/coverages/what-is-a-coverage.htm)
* [Oracle Spatial topology](https://docs.oracle.com/cd/B19306_01/appdev.102/b14256/sdo_topo_concepts.htm)
* [PostGIS Topology](http://postgis.net/docs/manual-2.3/Topology.html)
* [TopoJSON](https://github.com/topojson/topojson/wiki)
 - [Awesome dynamic simplification](https://bl.ocks.org/mbostock/6245977)

Note:
Topological data and capable software has been around for a long time.

One of the earliest implementations in this area that I know if was created by ESRI and was a part of their now discontinued product ARC/INFO. The implementation and format which was called "coverage" and was kept as a trade secret. The official story is that the current product line more or less has replaced the functionality that was available with ARC/INFO but I argue that it does not.

The next implementation I'm aware of is the result of a standardized effort which was made in the 90ies by OGC and implemented by Oracle as part of their Oracle Spatial offering. The publicly available documentation is a good technical source of how topological data works and how the model is implemented in detail.

Then we have PostGIS which implemented the same model as of version 2. I have used it many times and in my opinion it's a very roboust implementation with a large suite of unit and regression tests verifying correctness.

Lastly we have TopoJSON which was was developed my Mike Bostock, the creator of d3 which I'm sure you have heard of. He created TopoJSON as an efficient storage format but also for correct visualization. Let's look at his awesome dynamic simplification example (it's not an animation!)

---

### Why?

* Scratch an itch to learn more about the PostGIS Topology implementation
* Edit topological data without server communication

---

### API

* [Topolis](https://bjornharrtell.github.io/topolis/0.2.0/apidocs/)
* [PostGIS](http://postgis.net/docs/manual-2.3/Topology.html)

---

### Demonstration

* [OpenLayers example](http://openlayers.org)

Note: 
Demonstrate creating an edge, a face, splitting a face and deleting an edge.
Demonstrate the missing feature to heal edges, show https://github.com/bjornharrtell/topolis/blob/master/src/edge.js#L677.

---

### How?

* Entirely a manual port
* Depends on [rbush](https://github.com/mourner/rbush) from Mapbox/@mourner
 - getNodeByPoint, getEdgeByPoint, getEdgesByLine, getFaceByPoint
* Depends on [JSTS](https://github.com/bjornharrtell/jsts) for some of the needed geometrical algorithms
 - relate, intersects, polygonize

Note:
Would like to replace JSTS with something more light weight, but it not trivial.

---

### Is it ready?

* No
* Port the remaining functions from PostGIS
* Port the unit tests from PostGIS
* Big one: Find a solution to work with partial topology

Note:

I think at least porting the remaining functions and more complete testing is needed before using topolis in the real world.

Explain what I mean with partial topology. Can still be useful but will basically only work with small topologies.

---

### End!

![Logo](assets/images/twitter.png) [@bjornharrtell](https://twitter.com/bjornharrtell)