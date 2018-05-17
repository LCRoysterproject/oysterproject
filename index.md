---
output: 
  md_document:
    variant: markdown
---

![marsh](http://www.wec.ufl.edu/oysterproject/i/header_oysters.jpg)

# Project

The goal - keeping estuaries resilient in the face of global change. The primary goal of this project is to restore degraded chains of reefs in a way that is resilient both to sea level rise, and to continued low flows from the river. By so doing, we predict healthy reefs will buffer the estuaries from fluctuations in salinity, and from coastal erosion. The effects of this buffering should cascade to the fish, shellfish, birds and plant communities that humans care about, under a variety of future climate and 
sea level conditions.

You can read more about the project here : 
[R.E.E.F](http://www.wec.ufl.edu/oysterproject/restoration.php)

# Data Collection

## Water Quality Monitoring

Continous data are collected in nine sites with Star-Oddi and Diver sensors. The sites are located around the Lone Cabbage Reef in Cedar Key, FL. Discete measurements are also collected at these sites. Sensors are secured to the ocean bottom, and record continously every hour on the hour.     
These data are provisional raw downloads from instruments and subject to revision following QA/QC procedures.  
Temperature and salinity (estimated from conductivity measures) are recorded hourly using CT sensors at stations 2 and 4-9, and CTD sensors at stations 1 and 3.  

Sensor data site links are arranged in the order they lay near the Lone Cabbage Reef from North to South and West to East.  
[Site 6](http://rpubs.com/oysterproject/site6measurements),    [Site 1](http://rpubs.com/oysterproject/site1measurements),    [Site 7](http://rpubs.com/oysterproject/site7measurements)
  
[Site 5](http://rpubs.com/oysterproject/site5measurements), [Site 2](http://rpubs.com/oysterproject/site2measurements), [Site 8](http://rpubs.com/oysterproject/site8measurements) 
  
[Site 4](http://rpubs.com/oysterproject/site4measurements),  [Site 3](http://rpubs.com/oysterproject/site3measurements), [Site 9](http://rpubs.com/oysterproject/site9measurements)     

<img src="pic/lc_wq_map.jpg" width="55%" >

[Discrete lab results](http://rpubs.com/oysterproject/alllabresults) ,processed by Lakewatch UF, are available for Sites 1 through 6, for 2017.

[Salinity and temperature figures](http://rpubs.com/oysterproject/allsalplots) are available for all nine site locations.  

Site data can be compared in the [Shiny App](https://oysterprojectck.shinyapps.io/mels-shiny/).  

<img src="pic/20180417_sensor_algae.jpg" width="40%"> <img src="pic/20180417_collector_deploy2.jpg" width="40%">   
[(left) Steve B, Research Coordinator, retrieving a sensor covered in red algae, (right) spat collector being attached to a sensor deployment canister]  

## Oyster Bed Surveys and Proposed Reef

The proposed reef and oyster bed surveys can be viewed on the [Leaftlet Map](http://rpubs.com/oysterproject/map).

<img src="pic/lc_ pads_3d_2nd.JPG" width="40%" > <img src="pic/lc_pads_3d.JPG" width="40%" >  

[Images above are 3D renderings of proposed oyster reef]

## Oyster Sampling Efforts

Oyster sampling is all surveyed near and along Lone Cabbage Reef. Surveys are conducted using quadrats, transects, and counts. Data for these surveys are currently being analyzed. 

<img src="pic/IMG_2381.jpg" width="40%"> <img src="pic/IMG_2462.jpg" width="40%">  




  
    
![UF](http://branding.ifas.ufl.edu/media/brandingifasufledu/IFASWeb20132-300x99.png) ![WEC](http://www.wec.ufl.edu/awards/leadershipaward/_style/images/logo_wec.jpg)



<!DOCTYPE html>
<html>
<head>
  <title>leaflet-map-simple</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta charset="utf-8">

  <!-- Load Leaflet: instructions at http://leafletjs.com/download.html -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.1.0/dist/leaflet.css"
  integrity="sha384-Zh+y1U8o6/7ni8Mp8szvUfZjGeKKS10CGH3IlD6L1X+XwzYgQ1llOjw/Wslc0cma"
  crossorigin="anonymous">
  <script src="https://unpkg.com/leaflet@1.1.0/dist/leaflet.js"
  integrity="sha384-6rCYjRgWDEI2RlZxiVihj1WIZB/uvFiRCGpavTVgFrSPDL0Bk1AiqCW+mmv5h0LP"
  crossorigin="anonymous"></script>
  <!-- Load Omnivore plugin to convert CSV to GeoJSON format -->
  <script src='https://api.tiles.mapbox.com/mapbox.js/plugins/leaflet-omnivore/v0.3.1/leaflet-omnivore.min.js'></script>

  <!-- Position the map and title with Cascading Style Sheet (.css) -->
  <style>
  body { margin:0; padding:0; }
  #map {  position: absolute; top:0; bottom:0; right:0; left:0; }
  #map-title { position: absolute; margin-top: 10px; margin-left: 10px; float: bottom; background: white; border: 2px solid rgba(0,0,0,0.2); padding: 6px 6px; font-family: Helvetica; font-weight: bold; font-size: 30px; z-index: 200; }
  </style>
</head>
<body>

  <!-- Display the map and title with HTML division tags  -->
  <div id="map-title">Sensor Map</div>
  <div id="map"></div>

  <!-- Create the map content with JavaScript (.js) -->
  <script>
  /* Set up the map with initial center and zoom level */
  var map = L.map('map', {
    center: [29.25, -83.10], // EDIT latitude, longitude to re-center map
    zoom: 13,  // EDIT from 1 to 18 -- decrease to zoom out, increase to zoom in
    scrollWheelZoom: true
  });
  /* Control panel to display map layers */
  // var controlLayers = L.control.layers( null, null, {
  //  position: "topright",
  //  collapsed: false
  // }).addTo(map);
  /* Carto light-gray basemap tiles with labels */
  var light = L.tileLayer('https://cartodb-basemaps-{s}.global.ssl.fastly.net/light_all/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>, &copy; <a href="https://carto.com/attribution">CARTO</a>'
  }); // EDIT - insert or remove ".addTo(map)" before last semicolon to display by default
  // controlLayers.addBaseLayer(light, 'Carto Light basemap');
  /* Stamen colored terrain basemap tiles with labels */
  var terrain = L.tileLayer('https://stamen-tiles.a.ssl.fastly.net/terrain/{z}/{x}/{y}.png', {
    attribution: 'Map tiles by <a href="http://stamen.com">Stamen Design</a>, under <a href="http://creativecommons.org/licenses/by/3.0">CC BY 3.0</a>. Data by <a href="http://openstreetmap.org">OpenStreetMap</a>, under <a href="http://www.openstreetmap.org/copyright">ODbL</a>.'
  }).addTo(map); // EDIT - insert or remove ".addTo(map)" before last semicolon to display by default
  // controlLayers.addBaseLayer(terrain, 'Stamen Terrain basemap');
  /* Display a blue point marker with pop-up text */
  L.marker([29.266459979116917, -83.115749973803759]).addTo(map) // EDIT latitude, longitude to re-position marker
  .bindPopup('Site 1, Serial # V5602').bindLabel('Site 1, Serial # V5602'); 
  L.marker([29.24560303799808, -83.095912020653486]).addTo(map) 
  .bindPopup('Site 2, Serial # S9059').bindLabel('Site 1, Serial # V5602').addTo(map); // EDIT pop-up text message
  /* Upload Latitude/Longitude markers from data.csv file, show Title in pop-up, and override initial center and zoom to fit all in map */
  // var customLayer = L.geoJson(null, {
  //  onEachFeature: function(feature, layer) {
  //    layer.bindPopup(feature.properties.Title);
  //  }
  // });
  // var runLayer = omnivore.csv('data.csv', null, customLayer)
  // .on('ready', function() {
  //  map.fitBounds(runLayer.getBounds());
  // }).addTo(map);
  // controlLayers.addOverlay(customLayer, 'Markers from data.csv');
  </script>
</body>
</html>



