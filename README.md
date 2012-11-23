LeafletDemo
===========
Today we are learning how to to do some basic javascript mapping so in the script.js first we make a leaflet map with

```javascript
var m = L.map('map');
```
and then we set the center
```javascript
m.setView([42.2, -71], 8);
```
you can do that a couple other ways, be aware that the following things are are equivilent to the above. 
```javascript
var m = L.map('map').setView([42.2, -71], 8); 
// "chaining" it is what thats called
var m = new L.Map('map', {
    center: [42.2, -71],
    zoom: 8
});
/*that was a more traditional way of doing it, L.map(id,opt) is actually just function(id,opt){return new L.Map(id, opt)}*/
/*the "new" keyword means its creating a new object based on L.Map and the two pramaters are the id of where the map will go , which is map here, and and "object" aka key value pairs of different paramaters and their values */

```
next we add a layer, before we add it, we define some stuff
```javascript
var url = 'http://otile{s}.mqcdn.com/tiles/1.0.0/osm/{z}/{x}/{y}.jpeg';
```
this is the url template the z x and y within {brackets} are the zoom x and way that make up the url, the s is for subdomains, its complicated but some browsers will download the tiles faster if they are on different domains or subdomains.
```javascript
var attributionText = 'Tiles Courtesy of <a href="http://www.mapquest.com/">MapQuest</a> &mdash; Map data &copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors';
```
this is the attribution, it's always polite to attribute other peoples maps
```javascript
var mapquestSubdomains = '1234';
```
these are the subdomains one of those 4 numbers will be put in the s in the url, we could have also done:
```javascript
var url = 'http://{s}.mqcdn.com/tiles/1.0.0/osm/{z}/{x}/{y}.jpeg'
var mapquestSubdomains = ['otile1','otile2','otile3','otile4'];
```
then we can wrap it all together into a object
```javascript
var optionsObject = {
    attribution : attributionText,
    subdomains : mapquestSubdomains
}
```
then make the layer
```javascript
var mq=L.tileLayer(url, optionsObject);
```
and add it to the map
```javascript
mq.addTo(m);
```
if we wanted to we could have written that more complactly as:
```javascript
var m = L.map('map').setView([42.2, -71], 8),
    mq = L.tileLayer('http://otile{s}.mqcdn.com/tiles/1.0.0/osm/{z}/{x}/{y}.jpeg', {subdomains : '1234', attribution : 'Tiles Courtesy of <a href="http://www.mapquest.com/">MapQuest</a>'}).addTo(m);
```