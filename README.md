# Ley Lines Explorer

A mobile-friendly web map and installable Progressive Web App (PWA).

## Run locally
Geolocation and service workers require a secure context. From this folder run:

```bash
python -m http.server 8000
```

Then open http://localhost:8000. On a phone, deploy to an HTTPS host (for example, GitHub Pages, Netlify, or your own HTTPS server).

## Use
1. Open the app and select **My location**. Approve the browser's location permission.
2. Import a GeoJSON FeatureCollection using **Import GeoJSON**.
3. Select **Find nearest line**. The app calculates the shortest straight-line distance to the nearest point on any imported LineString or MultiLineString.
4. Use the map layer control to switch between OpenStreetMap and OpenTopoMap.
5. On a supported mobile browser, use **Install app** or the browser's Add to Home Screen command.

## Dataset format
Import a `.geojson` or `.json` FeatureCollection. Line features should use `LineString` or `MultiLineString` geometry. Optional properties:
- `name`: alignment name
- `source`: citation, publication, URL, or provenance note
- `status`: e.g. `historical claim`, `modern proposal`, `community-submitted`

Point features can represent landmarks. Add a `name` and `source` property where possible.

Example (illustrative schema only; coordinates are placeholders, not a claimed ley line):

```json
{
  "type": "FeatureCollection",
  "features": [{
    "type": "Feature",
    "properties": {
      "name": "Example proposed alignment",
      "source": "Add a verifiable source",
      "status": "unverified proposal"
    },
    "geometry": {
      "type": "LineString",
      "coordinates": [[-1.0, 5.0], [0.0, 6.0], [1.0, 7.0]]
    }
  }]
}
```

## Important data limitation
There is no universally accepted, scientifically validated global ley-line inventory. The application deliberately ships without fabricated global alignments. The map can display a dataset you provide or curate, and the nearest-line result is only as complete and reliable as that dataset.

## Technology and privacy
- Leaflet map with OpenStreetMap and OpenTopoMap tiles.
- Turf.js nearest-point-on-line calculation.
- GPS is requested only after the user clicks **My location**. Coordinates are processed in the browser and are not sent to an application backend by this starter app.
- Map tiles and JavaScript libraries are loaded from third-party CDNs; an internet connection is needed for the basemap and initial library load. The PWA caches the app shell, not the global map tiles or external libraries.
- For production, review tile-provider usage policies, add a suitable privacy notice, and host the app over HTTPS.
