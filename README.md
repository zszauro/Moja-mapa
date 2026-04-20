<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <meta name="mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <link rel="apple-touch-icon" href="https://cdn-icons-png.flaticon.com/512/854/854878.png">
    
    <title>Satelita Szefa</title>
    
    <script src="https://unpkg.com/maplibre-gl@latest/dist/maplibre-gl.js"></script>
    <link href="https://unpkg.com/maplibre-gl@latest/dist/maplibre-gl.css" rel="stylesheet" />
    
    <style>
        body { margin: 0; padding: 0; overflow: hidden; }
        #map { position: absolute; top: 0; bottom: 0; width: 100%; }
        /* Dodajemy ładną ramkę dla przycisków */
        .maplibregl-ctrl-group { border: none !important; box-shadow: 0 0 10px rgba(0,0,0,0.5) !important; }
    </style>
</head>
<body>
    <div id="map"></div>
    <script>
        const klucz = 'RXqehBn2Ora8xhgt9MQY';

        const map = new maplibregl.Map({
            container: 'map',
            // Tutaj ustawiłem styl satelitarny
            style: `https://api.maptiler.com/maps/satellite/style.json?key=${klucz}`,
            center: [19.1451, 52.2370],
            zoom: 6,
            pitch: 45 // Lekkie pochylenie mapy dla efektu 3D
        });

        // Przyciski plus/minus
        map.addControl(new maplibregl.NavigationControl());
        
        // Przycisk "Gdzie jestem?"
        map.addControl(new maplibregl.GeolocateControl({
            positionOptions: { enableHighAccuracy: true },
            trackUserLocation: true,
            showUserLocation: true
        }));
