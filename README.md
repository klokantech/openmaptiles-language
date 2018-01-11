# OpenMapTiles language

This small javascript library adds support for changing language of [OpenMapTiles](https://openmaptiles.com/)-based maps displayed with [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/api/).

## Usage

Place this code ***AFTER*** loading mapbox-gl-js:
```html
<script src="https://cdn.klokantech.com/openmaptiles-language/v1.0/openmaptiles-language.js"></script>
```

## API

When the script above is loaded, it adds these methods to every `mapboxgl.Map` instance:

- `map.setLanguage(languageCode, noAlternatives)`
   - `languageCode` - language to use (see https://github.com/openmaptiles/openmaptiles/blob/master/openmaptiles.yaml for the possible values); use `"native"` to show names in local languages
   - `noAlternatives` (optional) - disable latin alternatives for non-latin languages (and vice-versa)

- `map.autodetectLanguage(fallback)`
  - Automatically detects language from browser (`navigator.language`) and uses that language
  - `fallback` (optional) - language to use if detection was not successful

## Complete example
```html
<html>
<head>
  <link href="https://cdn.klokantech.com/mapbox-gl-js/v0.43.0/mapbox-gl.css" rel="stylesheet" />
  <script src="https://cdn.klokantech.com/mapbox-gl-js/v0.43.0/mapbox-gl.js"></script>
  <script src="https://cdn.klokantech.com/openmaptiles-language/v1.0/openmaptiles-language.js"></script>
  <style>
    #map {position:absolute; top:0; right:0; bottom:0; left:0;}
    button {position:relative;z-index:1;}
  </style>
</head>
<body>
  <div id="map"></div>
  <button onclick="map.setLanguage('native')">Local language</button>
  <button onclick="map.setLanguage('de')">German</button>
  <button onclick="map.setLanguage('fr')">French</button>
  <button onclick="map.setLanguage('ja')">Japanese</button>
  <button onclick="map.setLanguage('ja', true)">Japanese (no latin alternative)</button>
  <script>
    var map = new mapboxgl.Map({
      container: 'map',
      style: 'https://maps.tilehosting.com/styles/basic/style.json?key=[key]',
      center: [8.55, 47.37],
      zoom: 4
    });
    map.autodetectLanguage(); // automatically detect from browser
  </script>
</body>
</html>
```
