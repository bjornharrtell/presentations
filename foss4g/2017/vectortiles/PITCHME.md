## Topolis

---

### Introduction

* Björn Harrtell
* Septima P/S
* [JSTS](http://bjornharrtell.github.io/jsts/)

Note:
Might know me as the author of the JavaScript port of JTS called JSTS.

---

## Subject

* JavaScript library to manipulate topological data
* Ported from PostGIS Topology implementation

---

## Typical topological data

* Road networks built from nodes and edges
* Administrative or geographic areas adding the concept of surfaces or faces

Note:
Geographical data that we see today is often a collection of individual points, lines or polygons without topological relation. This is a simple model but can cause quality issues if 

---

## Prior art

* [ESRI ArcInfo Coverage format](http://desktop.arcgis.com/en/arcmap/10.3/manage-data/coverages/what-is-a-coverage.htm)
* [Oracle Spatial topology](https://docs.oracle.com/cd/B19306_01/appdev.102/b14256/sdo_topo_concepts.htm)
* [PostGIS Topology](http://postgis.net/docs/manual-2.3/Topology.html)
* [TopoJSON](https://github.com/topojson/topojson/wiki)
 - [Awesome dynamic simplification](https://bl.ocks.org/mbostock/6245977)

Note:
The earliest implementation of topological data structure for geographical purposes that I know if was created by ESRI and included in their now discontinoued product ArcInfo. The implementation and format which was called "coverage" was never publicly documented and ESRI themselves seems to have given up on handling topological data.

A standardized effort was made in the 90ies by OGC and implemented by Oracle as part of their Oracle Spatial offering. Their publicly available documentation is a good technical source of how topological data works and how the model is implemented in detail.

PostGIS, or rather core developer Sandro Santilli, implemented the same model as of verison 2.0. The documentation is of reference nature and assumes knowledge of topological concepts, but the implementation is roboust and has a large suite of unit tests verifying correctness.

TopoJSON was developed my Mike Bostock who I'm sure you have heard of as he is the author of d3. He created TopoJSON as an efficient storage format but also for correct visualization. Let's look at his awesome dynamic simplification example (it's not an animation!)

---

## Why?

* Why a JavaScript library to manipulate topological data?
* For fun
* Client based "offline" editing of topological data

Note:
Like JSTS, I made topolis by porting existing code and as an experiment to see how well it could work. But it might become useful for cases where you need to have a pure client based logic, for instance if the client needs to work in offline mode.

---

## Demonstration

* [OpenLayers example](http://openlayers.org)

Note: 
Incomplete https://github.com/bjornharrtell/topolis/blob/master/src/edge.js#L677

---

## How?

* Manual work
* Uses JSTS for some of the needed geometrical algorithms

---

## Is it done yet?

* No