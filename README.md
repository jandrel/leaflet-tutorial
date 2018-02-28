# leaflet-tutorial
Files for use in LEADR tutorial
## Fork this repo
## Set this repo's Pages branch to "master"
## Edit index.html add a ine below the paragraph
```html
<div id="map" style="height: 400px"></div>
  ```
## Add this stylesheet to head
```html
<link rel="stylesheet" type="text/css" href="leaflet/leaflet.css">
```
## Add these scripts to body, just above end of `body`
```html
<script src="https://code.jquery.com/jquery-3.3.1.js" integrity="sha256-2Kok7MbOyxpgUVvAk/HJ2jigOSYS2auK4Pfzbm7uH60=" crossorigin="anonymous"></script>
<script src="leaflet/leaflet.js"></script>
```
## Write new script, just below the ones pasted in (still inside `body`)
```html
<script type="text/javascript">
        
</script>
```
## Add the function calling the map to the new script
```javascript
var map = L.map('map').setView([42.7322281,-84.4870938], 15);
```
At this point, if you save index.html and load the page in a browser tab, you'll see a map with no tiles. 
## Add a tilelayer to the called map, in the same script container
```javascript
L.tileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors, example by Brian'
}).addTo(map);
```
Note the attribution, which will add itself to the bottom-right attribution on the map. Notice the final funtion, telling it to add itself to the map, that's already been initialized.

