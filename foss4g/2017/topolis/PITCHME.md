## Topolis

---

### Introduction

* Björn Harrtell
* Septima P/S
* [JSTS](http://bjornharrtell.github.io/jsts)

Note:
Present myself.
I'm the author of the JavaScript port of Java Topology Suite called JSTS, used in amongst other things Turf from MapBox.

---

### Subject

* Topolis
* JavaScript library to manipulate topological data
* Ported from PostGIS Topology implementation

Note:
So this presentation is about a small side project of mine called Topolis.

---

### Typical topological data

* Built from simple geometry but with toplogical constraints
* Road networks built from nodes and edges
* Add the concept face (surface) commonly used for administrative or geographic areas

Note:
Simple geometry is usually defined as individiual points, lines or polygons.
An example of a toplogical contraint is that no edge may overlap another edge.

---

### Prior art

* <a target="_blank" href="http://desktop.arcgis.com/en/arcmap/10.3/manage-data/coverages/what-is-a-coverage.htm">ESRI ArcInfo Coverage format</a>
* <a target="_blank" href="https://docs.oracle.com/cd/B19306_01/appdev.102/b14256/sdo_topo_concepts.htm">Oracle Spatial topology</a>
* <a target="_blank" href="http://postgis.net/docs/manual-2.3/Topology.html">PostGIS Topology</a>
* <a target="_blank" href="https://github.com/topojson/topojson/wiki">TopoJSON</a>
 - <a target="_blank" href="https://bl.ocks.org/mbostock/6245977">Awesome dynamic simplification</a>

Note:
The earliest implementation of topological data structure for geographical purposes that I know if was created by ESRI and included in their now discontinoued product ArcInfo. The implementation and format which was called "coverage" and was kept as a trade secret.

A standardized effort was made in the 90ies by OGC and implemented by Oracle as part of their Oracle Spatial offering. Their publicly available documentation is a good technical source of how topological data works and how the model is implemented in detail.

PostGIS, or rather core developer Sandro Santilli, implemented the same model as of verison 2.0. The documentation is of reference nature and assumes knowledge of topological concepts, but the implementation is roboust and has a large suite of unit tests verifying correctness.

TopoJSON was developed my Mike Bostock who I'm sure you have heard of as he is the author of d3. He created TopoJSON as an efficient storage format but also for correct visualization. Let's look at his awesome dynamic simplification example (it's not an animation!)

---

### Why?

* Scratch itch to learn PostGIS topology implementation
* Edit topological data without server communication

---

### API

* [Topolis](https://bjornharrtell.github.io/topolis/0.2.0/apidocs/)
* [PostGIS](http://postgis.net/docs/manual-2.3/Topology.html)

---

### Demonstration

* <a target="_blank" href="http://openlayers.org">OpenLayers example</a>

Note: 
Demonstrate creating an edge, a face, splitting a face and deleting an edge.
Demonstrate the missing feature to heal edges, show https://github.com/bjornharrtell/topolis/blob/master/src/edge.js#L677.

---

### How?

* Manual work
* Depends on rbush from MapBox/@mourner
 - getNodeByPoint, getEdgeByPoint, getEdgesByLine, getFaceByPoint
* Depends on JSTS for some of the needed geometrical algorithms
 - intersects, polygonize

Note:
Would like to replace JSTS with something more light weight.

---

### Is it done yet?

* No
* Port the remaining functions from PostGIS
* Port the unit tests from PostGIS
* Big one: Find a solution to work with partial topology

Note:

Explain what I mean with partial topology.