---
marp: true
theme: uncover
---

# FlatGeobuf

---

Björn Harrtell
Septima P/S 4 år
SWECO 10 år

---

Började på smått på det för tre år sedan. 

<!--
Fick idén för att jag inte tyckte det fanns någon värdig ersättare för shapefil men också bara för att det var kul och jag ville lära mig med om hur det fungerar med till exempel spatialt index.
-->

* 1.0.0 - aug 2019
* 2.0.0 - nov 2019
* 3.0.0 - jan 2020

---

* GDAL 3.1.0 (maj 2020)
* QGIS 3.16 (okt 2020)

<!--
En milstolpe var att jag fick gjort implementation i GDAL 3.1.0 (maj 2020) som var en förutsättning för att få det att fungera i QGIS 3.16 (okt 2020)
-->

---

#### Externa bidrag

* Logo (dee-y) (https://github.com/flatgeobuf/flatgeobuf/issues/2)
* Rust (Pirmin Kalberer)
* TypeScript/JavaScript förbättringar (Michael Kirk)

<!--
Jag har fått signifikanta bidrag från flera personer. Bland annat en full referensimplementation i Rust samt förbättringar i TypeScript/JavaScript referensimplementation.
-->

---

Exempel: https://flatgeobuf.org/examples/leaflet/large.html

---

* GeoPackage?

<!--
Varför är inte GeoPackage en värdig ersättare? Det kan man ha delade meningar om men ett tekniskt problem med GeoPackage är att det inte är välägnat maskin till maskin kommunikation. Det går till exempel inte att läsa eller skriva GeoPackage i en ström.
-->
