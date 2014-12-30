---
layout: post
title: Leonardo da Vinci&#39;s very accurate map of Imola
---

<script src='https://api.tiles.mapbox.com/mapbox.js/v2.1.4/mapbox.js'></script>
<link href='https://api.tiles.mapbox.com/mapbox.js/v2.1.4/mapbox.css' rel='stylesheet' />

  <div id='map'></div>
  <input id='range' class='range' type='range' min='0' max='1.0' step='any' />

  <section class="intro column">
    <p><span class="first">...V</span>ery accurate indeed, and very beautiful I would suggest. I love old maps and their power in revealing the changes of the land over time, but I must admit, I never heard of this one until recently.</p>
    <p>It was my five year old son that brought me to it. We have an old book on Leonardo and this Christmas he was looking at it and, because I saw him curious, I searched the Web for more and there, on a <a href="http://en.wikipedia.org/wiki/Leonardo_da_Vinci">wikipedia page</a>, I found it! (more details can also be found <a href="https://www.google.com/culturalinstitute/asset-viewer/plan-of-imola/hgEpMgZ5mn6R4A">here</a>)</p>
    <p class="italic">&#34;Leonardo created a map of Cesare Borgia's stronghold, a town plan of Imola in order to win his patronage. Maps were extremely rare at the time and it would have seemed like a new concept. Upon seeing it, Cesare hired Leonardo as his chief military engineer and architect.&#34;</p>
    <p>What a hell of a work for a job application! It looked so accurate I couldn't resist and I started comparing the map with an aerial image and tried explaining to my son the changes of the landscape over time. This post is the polished version of that improvised lecture and the above interactive map application is my small homage to such an ingenious man.</p>
  </section>

  <section class="main column">
    <p><span class="first">S</span>o, what has changed, or hasn't, in five centuries in and around this small town in central Italy? Before I go any further, let me say that I know nothing about the history of Imola and all I write are simple deductions, and sometimes guesses, from looking at the maps. To make this clear, this article opens with an interactive map application I encourage anyone to play with: zoom in and out, swipe (use range bar below map), pan, turn on and off the different layers (hover over top-right icon on map). In other words, allow yourself some time, explore and see for yourself how powerful maps can be.</p>
    <p>Maybe the most obvious statement is that the old town has changed very little and the beautiful map of Leonardo does a very good job in depicting this. The castle, for instance has not changed a bit, although two near towers are now in ruins. But the castle is not alone: churches, squares, colonnades, palaces, buildings, the shape of the roads. In some cases it is even possible to recognize the same courtyards and gardens, unchanged over five centuries. Such is the richness in detail of the antique map and such is the abundance of features that have not changed, that geo-referencing it was a very easy and fast task.</p>
    <p>And now a few words about what has changed. The most obvious transformation is the expansion of the town. Note that the light beige-okra colour, that occupies most of the outside region of the map, symbolizes cultivated fields. Nowadays, although the surrounding region is still very agricultural, there are no fields left within the boundaries of Leonardo's map. You can notice a few gardens and playgrounds, but no fields.</p>
    <p>A somehow less obvious change is the disappearance of the town defensive walls, moat and fortified doors. This, without any other information, looks like a very mysterious disappearance, especially if you think how many Italian towns still bare some version of their antique defensive architecture.</p>
    <p>A quick <a href="http://temi.comune.imola.bo.it/riqualifica/porta_montanara/mura.htm">search on the Internet</a> tells us that the walls depicted in the map were terminated between 1453-60, so they were just few years older of the map itself. Sadly, the walls and the moat will stand for more than 400 years, only to be destroyed at the beginning of the twentieth century to make room for the expansion of the town.</p>
    <p>One last interesting observation can be made about the position and shape of the river in the lower side of the map. This, unlike the old buildings, is heavily mispositioned in respect to its current course. Two ideas come to mind. First, it is possible that Leonardo did not put much effort in depicting the river's position because his main focus was on the town. But there could be another possibility: that the river has changed position over the centuries. The truth is probably somewhere in the middle.</p>
    <p>Inaccurate or not, there is still a lot to learn by comparing the river on the different maps. Can you see how the river's course is somehow straighter and tighter these days? Leonardo's river was more meanderous, wider and its boundaries more blurred. This is consistent with how rivers used to be, free to flow and to flood.</p>
  </section>

  <footer>
    <p>For details about the map application look into the <a href="https://github.com/deciob/imola">github repository</a></p>
  </footer>

<script>
(function() {
'use strict';

// see:
// https://www.mapbox.com/mapbox.js/example/v1.0.0/toggle-baslayers/
// https://www.mapbox.com/mapbox.js/example/v1.0.0/swipe-layers/

L.mapbox.accessToken = 'pk.eyJ1IjoiZGVjaW9iIiwiYSI6ImhuRG9vRDAifQ.mgXBdBFSOgGJaeEggvGISg';

var layerLeo,
    layerEsri,
    layerLeonardo,
    map,
    baseMaps,
    overlayMaps,
    southWest,
    northEast,
    bounds,
    leoSouthWest,
    leoNorthEast,
    leoBounds,
    range,
    CartoDB_PositronNoLabels,
    Acetate_roads;

leoSouthWest = L.latLng(44.342, 11.724),
leoNorthEast = L.latLng(44.363, 11.7),
leoBounds = L.latLngBounds(leoSouthWest, leoNorthEast);

CartoDB_PositronNoLabels = L.tileLayer('http://{s}.basemaps.cartocdn.com/light_nolabels/{z}/{x}/{y}.png', {
  attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a> &copy; <a href="http://cartodb.com/attributions">CartoDB</a>',
  subdomains: 'abcd',
  minZoom: 14,
  maxZoom: 18
});

Acetate_roads = L.tileLayer('http://a{s}.acetate.geoiq.com/tiles/acetate-roads/{z}/{x}/{y}.png', {
  attribution: '&copy;2012 Esri & Stamen, Data from OSM and Natural Earth',
  subdomains: '0123',
  minZoom: 14,
  maxZoom: 18
});


layerLeo = L.mapbox.tileLayer('deciob.098d5e15');
layerEsri = L.tileLayer('http://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
  attribution: 'Tiles &copy; Esri &mdash; Source: Esri, i-cubed, USDA, USGS, AEX, GeoEye, Getmapping, Aerogrid, IGN, IGP, UPR-EGP, and the GIS User Community'
});
layerLeonardo = L.tileLayer('{{ site.url }}/assets/tiles/{z}/{x}/{y}.png', 
  {tms: true, bounds: leoBounds});

// Construct a bounding box for this map that the user cannot move out of
southWest = L.latLng(44.338, 11.669),
northEast = L.latLng(44.369, 11.752),
bounds = L.latLngBounds(southWest, northEast);

map = L.mapbox.map('map', null, 
  {maxBounds: bounds, maxZoom: 17, minZoom: 14}).setView([44.353, 11.713], 15);

baseMaps = {
  "Aerial ESRI": layerEsri,
  "CartoDB Positron": CartoDB_PositronNoLabels,
  "OSM Leonardo inspired": layerLeo
};
overlayMaps = {
  "Map of Leonardo da Vinci": layerLeonardo,
  "Acetate Roads": Acetate_roads,
};

baseMaps['CartoDB Positron'].addTo(map);
overlayMaps['Map of Leonardo da Vinci'].addTo(map);
L.control.layers(baseMaps, overlayMaps).addTo(map);

range = document.getElementById('range');

function clip() {
  var nw = map.containerPointToLayerPoint([0, 0]),
      se = map.containerPointToLayerPoint(map.getSize()),
      clipX = nw.x + (se.x - nw.x) * range.value;
  layerLeonardo.getContainer().style.clip = 'rect(' + [nw.y, clipX, se.y, nw.x]
    .join('px,') + 'px)';
}

range['oninput' in range ? 'oninput' : 'onchange'] = clip;
map.on('move', clip);
map.on('layeradd', clip);

clip();
})();
</script>
