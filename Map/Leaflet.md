# Leaflet (MAP)

Librairie :

```
https://unpkg.com/browse/leaflet@1.9.4/
```

#### Integration

```SQL
		-- geom : POINT(Lat, Long)
        SELECT
        JSONB_BUILD_OBJECT(
          'type', 'Feature',
          'properties', JSONB_BUILD_OBJECT(
              'garbageCollectionCode',garbage_collection_code
          )
          ,'geometry',st_asgeojson( ST_Collect(ST_MakeLine(geom order by "time"),ST_Collect(geom order by"time")))::JSONB
          ,'id', to_jsonb(concat(garbage_collection_code,'-',time::date)::text)
        )
        FROM
          lifting_view lv WHERE  lv.contract_id = 'db91983f-aa36-4c92-bab5-525a04a033b2' 
          AND lv.garbage_collection_code IN (:codde)  
          GROUP BY    garbage_collection_code,      time::date
```

```php
        # 'Content-Type' => 'application/geo+json'
        $response = $manager->getJSONB_BUILD_OBJECT($parameters);

        // prepare geojson leaflet structure
        $data = [
            "type" => "FeatureCollection",
            "features" => $response
        ];

        return new JsonResponse($data , Response::HTTP_OK, ['Content-Type' => 'application/geo+json']);
```


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
Result :

![image](https://github.com/ADCPD/ADCPD/assets/10563431/45462906-bf41-4a72-b2ae-dfd86f65aaa5)
