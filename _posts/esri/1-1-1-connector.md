---
title: Connector
tags: esri touch
layout: control
---

<div class='demo-map claro' id='map-div'></div>

Like Google's API, ESRI's is closed-source and requires you to include it from
a remote server. That looks like:

<pre class='prettyprint'>
&lt;script
  type='text/javascript'
  src='http://serverapi.arcgisonline.com/jsapi/arcgis/?v=2.8'&gt;&lt;/script&gt;
&lt;link
  rel='stylesheet'
  type='text/css'
  href='http://serverapi.arcgisonline.com/jsapi/arcgis/2.8/js/dojo/dijit/themes/claro/claro.css'&gt;
</pre>

ESRI's code is a bit odd: by default mouse wheel scrolling pans north and south
rather than zooming. Like [OpenLayers](http://mapbox.com/wax/connector-ol.html),
it has a rather obtuse obsession with projections, but to the point that
one cannot simply reproject in-browser, as OpenLayers does with its native code
and [proj4js](http://trac.osgeo.org/proj4js/), but it relies on an
external server to do this work.

You'll also need to add the class `claro` to div your map will live in,
so that the 'claro' stylesheet affects it.

<pre class='prettyprint live'>
var url = 'http://api.tiles.mapbox.com/v3/mapbox.geography-class.jsonp';
wax.tilejson(url, function(tilejson) {
   var map = new esri.Map('map-div', {
     extent: new esri.geometry.Extent(-13686470.64, 5203830.72, -13669270.31, 5215290.28,
     new esri.SpatialReference({
       wkid: 3857
     }))
   });

   map.addLayer(new wax.esri.connector(tilejson));
});
</pre>