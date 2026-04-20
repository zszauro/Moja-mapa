<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <title>Mapa Arti Satelita</title>
    <script src="https://unpkg.com/maplibre-gl@latest/dist/maplibre-gl.js"></script>
    <link href="https://unpkg.com/maplibre-gl@latest/dist/maplibre-gl.css" rel="stylesheet" />
    <style>
        body, html { margin: 0; padding: 0; height: 100%; background: #000; }
        #map { position: absolute; top: 0; bottom: 0; width: 100%; }
        .ui { position: absolute; top: 10px; left: 10px; z-index: 10; }
        button { padding: 15px; background: white; border: 3px solid black; border-radius: 10px; font-weight: bold; }
    </style>
</head>
<body>
    <div class="ui"><button onclick="lokalizacja()">MOJA POZYCJA</button></div>
    <div id="map"></div>
    <script>
        // KOD NAPRAWIAJĄCY BŁĘDY KLAWIATURY:
        // Niezależnie od tego, czy wkleisz dużą czy małą literę, system wymusi małe 'm'
        const surowyKlucz = "MK4tFjD8oPZF7XZiiGBc"; 
        const poprawnyKlucz = "m" + surowyKlucz.substring(1);

        const map = new maplibregl.Map({
            container: 'map',
            style: 'https://api.maptiler.com/maps/satellite/style.json?key=' + poprawnyKlucz,
            center: [19.14, 52.23],
            zoom: 6
        });

        function powiedz(t) {
            const m = new SpeechSynthesisUtterance(t);
            m.lang = 'pl-PL';
            window.speechSynthesis.speak(m);
        }

        function lokalizacja() {
            navigator.geolocation.getCurrentPosition(p => {
                const pos = [p.coords.longitude, p.coords.latitude];
                map.flyTo({center: pos, zoom: 17});
                powiedz("Szefie, jesteś tutaj. Satelita Cię widzi.");
                new maplibregl.Marker({color: 'red'}).setLngLat(pos).addTo(map);
            }, () => {
                alert("Włącz GPS!");
            });
        }

        map.addControl(new maplibregl.NavigationControl());
        map.on('load', () => {
            powiedz("Satelita gotowa. Czekam na rozkazy, Szefie.");
        });
    </script>
</body>
</html>


