LeafletSlider
=============

The [Leaflet](http://leafletjs.com/) Time-Slider enables you to dynamically add and remove Markers on a map by using a [JQuery UI slider
](http://jqueryui.com/slider/).


Check out the [Demo](https://falke-design.github.io/LeafletSlider/)!

With two silders [Epoch.html](https://falke-design.github.io/LeafletSlider/examples/epoch.html)!

Popup Demo: [Popup.html](https://falke-design.github.io/LeafletSlider/examples/popup.html)

Usage
-----
Add:
* ``SliderControl.js`` [CDN](https://cdn.jsdelivr.net/gh/Falke-Design/LeafletSlider@latest/dist/leaflet.SliderControl.min.js)
* [JQuery](https://cdnjs.com/libraries/jquery)
* [JQueryUI](https://cdnjs.com/libraries/jqueryui)

to your normal Leaflet map.




To enable the Slider you have to pass in a layer to the SliderControl, add the Slider.
The Control has to be initialized by using the method startSlider(); on the control.

```javascript
//Create a marker layer (in the example done via a GeoJSON FeatureCollection)
var testlayer = L.geoJson(json);
var sliderControl = L.control.sliderControl({position: "topright", layer: testlayer});

//Make sure to add the slider to the map ;-)
map.addControl(sliderControl);

//And initialize the slider
sliderControl.startSlider();
````

The layers must have the following structure:

`layer.options.time = ` (if timeAttribute is `time`)

`layer.feature.properties.time = ` (if timeAttribute is `time`)

#### Options
| Option | Default | Description |
|---|---|---|
| position | 'topright' | The position of the Slider |
| layer | null | **Required** The layergroup with the layers (markers) |
| timeAttribute | 'time' | The attribute for the slider |
| isEpoch | false | Whether the time attribute is seconds elapsed from epoch |
| startTimeIdx | 0 | Where to start looking for a timestring|
| timeStrLength | 19  | the size of  yyyy-mm-dd hh:mm:ss - if millis are present this will be larger |
| maxValue | -1 | The max value of the slider |
| minValue | 0 | The min value of the slider |
|showAllOnStart| false | Show all layers on start|
|range| false | To enable the range slider|
| follow | 0 | To show only the last n layers, 0 means show all previous markers |
|sameDate| false | Show only all markers with the current date|
|alwaysShowDate| false | Show allways the date box|
|rezoom| null | You can use the rezoom property to ensure the markers being displayed remain in view. The integer value will be the maximum zoom level.|
|orderMarkers| true| Orders the markers by the timeAttribute |
|orderDesc| false | Order the markers descending (only work if orderMarkers is true)|
|popupContent| ' ' | Custom popup content if marker has no popup|
|popupOptions| {} | Popup options for markers with no default popup [popup-options](https://leafletjs.com/reference-1.6.0.html#popup-l-popup)|
|showAllPopups| true | To show all popups, instead of one. Same as popup option "autoClose: false"|
|showPopups| true | To open popups of the markers|


Add options on creating the control
```javascript
var sliderControl = L.control.sliderControl({options});
```

#### Mixed features 

The Leaflet Slider can also be used for usual LayerGroups with mixed features (Markers and Lines, etc.)
```javascript
var marker1 = L.marker([51.5, -0.09], {time: "2013-01-22 08:42:26+01"});
var marker2 = L.marker([51.6, -0.09], {time: "2013-01-22 10:00:26+01"});
var marker3 = L.marker([51.7, -0.09], {time: "2013-01-22 10:03:29+01"});

var pointA = new L.LatLng(51.8, -0.09);
var pointB = new L.LatLng(51.9, -0.2);
var pointList = [pointA, pointB];

var polyline = new L.Polyline(pointList, {
    time: "2013-01-22 10:24:59+01",
    color: 'red',
    weight: 3,
    opacity: 1,
    smoothFactor: 1
});


layerGroup = L.layerGroup([marker1, marker2, marker3, polyline ]);
var sliderControl = L.control.sliderControl({layer:layerGroup});
map.addControl(sliderControl);
sliderControl.startSlider();
````

#### Event
You can listen on the slider if range has changed.
```javascript
sliderControl.on('rangechanged',function (e) {
    console.log(e.markers);
});
```
Returns the visible markers.


#### Touch Support
For touch support add:
```javascript
<script src="https://cdnjs.cloudflare.com/ajax/libs/jqueryui-touch-punch/0.2.3/jquery.ui.touch-punch.min.js"></script>
````

Bower
----
Leaflet Slider is also a registered package in [Bower](http://bower.io/) (based on [nodejs](http://nodejs.org/)). Integrate the source in your project with:
```
npm install -g bower
bower install leaflet-slider
```




Author
-----
Dennis Wilhelm, 2013

Updated by @Falke-Design 2020