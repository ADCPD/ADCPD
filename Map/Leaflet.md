# Leaflet (MAP)

Librairie :

```
https://unpkg.com/browse/leaflet@1.9.4
```

#### Integration

```html
<div class="container-fluid" onload="prepareCollectionMadeCartography()">
  <div id="map" class="flows-container"></div>
</div>
<script type="text/javascript">
    $(document).ready(function () {
        prepareCollectionMadeCartography();
    });

    function prepareCollectionMadeCartography() {
        const collecteInfo = $('#collecte_detail_page').attr('data-content');
        let collecteInfoArray = collecteInfo.split("#");
        let contractId = collecteInfoArray[0];
        let collecteCode = collecteInfoArray[1];

        const geoJsonUrl = Routing.generate('incitative_communication_collecte_cartography', {
            contractId: contractId,
            codeCollecte: collecteCode
        });

        map = L.map('map').setView([0, 0], 5);
        let mapTemplate =  'https://cartodb-basemaps-{s}.global.ssl.fastly.net/light_all/{z}/{x}/{y}.png';
        // Set up the OSM layer
        L.tileLayer(
            mapTemplate, {
                maxZoom: 18
            }).addTo(map);

        $.ajax({
            type: "GET",
            url: geoJsonUrl,
            dataType: 'json',
            success: function (response) {
                let geojsonLayer = L.geoJson(response, {
                    onEachFeature: function (feature, layer) {
                        feature.properties.bounds_calculated = layer.getBounds().toBBoxString();
                     }
                }).addTo(map);
                map.fitBounds(geojsonLayer.getBounds());
                $("#info").fadeOut(500);
            }
        });
    }
```
