# leaflet-tutorial
Files for use in LEADR tutorial. The [Leaflet JS library can be found here](http://leafletjs.com/download.html). Sign up for a [Mapbox account here](https://mapbox.com). Leaflet has a [quick start guide](http://leafletjs.com/examples/quick-start/). Leaflet's more complete [documentation is here](http://leafletjs.com/reference-1.3.0.html).
## Fork this repo
## Set your forked repo's Pages branch to "master"
## Edit index.html to add a ine below the paragraph
```html
<div id="map-here" style="height: 400px"></div>
  ```
## Add this stylesheet to head
```html
<link rel="stylesheet" type="text/css" href="leaflet/leaflet.css">
```
## Add these scripts to `body`, just above end of `body`
```html
<script src="https://code.jquery.com/jquery-3.3.1.js" integrity="sha256-2Kok7MbOyxpgUVvAk/HJ2jigOSYS2auK4Pfzbm7uH60=" crossorigin="anonymous"></script>
<script src="leaflet/leaflet.js"></script>
```
## Write new script, just below the ones just pasted in (still inside `body`)
```html
<script type="text/javascript">
        
</script>
```
## Add the function calling the map to the new script
```javascript
var map = L.map('map-here').setView([42.7322281,-84.4870938], 17);
```
At this point, if you save index.html and load the page in a browser tab, you'll see a map with no tiles. In this code, the browser will use the L.map function to create a map in the map variable, which is tied to the map-here ID in the html code. The view is set to center on that latitude and longitude, and the view is set to the 17th level (higher level numbers are closer in on the map).
## Add a tile layer to the initialized map, in the same script container
```javascript
L.tileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="http://mapbox.com">Mapbox</a> simple streets; example by Brian'
}).addTo(map);
```
Note the attribution, which will add itself to the bottom-right attribution on the map. Notice the final funtion, telling it to add itself to the map that's already been initialized. The `addTo()` part is telling the browser to add the tile layer to the variable that is named "map" in the script. If you change the variable's name (some tutorias use "mymap"), the referenced variable in the `addTo()` function will need to be changed too.
## Swap out OpenStreetMaps for Mapbox
Change url inside L.tileLayer to
```javascript
https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token={accessToken}
```
Notice the variables `{id}` and `{accessToken}`. You'll need to provide values to those variables, in the same way that the map's `attribution` is provided. Get these from your own Mapbox account. Add a comma to the end of the `attribution` line, then add these two lines below that:
```javascript
id: '{your mapbox map id}',
accessToken: '{your mapbox access token}'
```
Leave the single quotes, but replace the values with your own. Or, use one of [Mapbox's public styles](https://www.mapbox.com/api-documentation/#maps), like `mapbox.streets-basic`.
## Common parameters
You can add other common variables to the same section as `attribution`, `id`, and `accessToken`, such as `minZoom` (the furthest out a map can display), `maxZoom` (the furthest in), and others (see [full documentation](http://leafletjs.com/reference-1.3.0.html)).
## Set Boundaries
Set the map boundaries, so that the user can't scroll the map to another part of the world. Start by defining two new variables just above `map`, with their values using the LatLng function to define two points with latitude and longitude:
```javascript
var northwest = L.latLng(42.75, -85);
var southeast = L.latLng(42.7, -84);
var bounds = L.latLngBounds(northwest, southeast);
```
Then, add the following betweem the `)` and `.` in `L.map('map').setView(` so the line now looks like this:
```javascript
L.map('map').setMaxBounds(bounds).setView([42.732224, -84.478351], 17);
```
## Add Marker with popup content
Create a marker with a popup by adding this new code inside the same script container, below everything else.
```javascript
var popupImg = "https://farm7.static.flickr.com/6223/6240985827_66d54a66b2_b.jpg",
    popupTitle = "LEADR",
    popupLoc = "Old Horticulture",
    content = "<img src=" + popupImg + " style='float:left;width:200px'padding-right:10px'><strong>" + popupTitle + "</strong><br>" + popupLoc + "<div style='clear:both'></div>",
    marker = L.marker([42.732217, -84.478339]).addTo(map);
    marker.bindPopup(content, {minWidth: 400, autoPanPadding: [5,5], closeButton: true});
```
