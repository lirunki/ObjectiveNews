# Image sources

Local SVGs in this folder are original schematics so pages work offline.

Story pages also hotlink **Wikimedia Commons** files via `Special:FilePath` (CORS: `Access-Control-Allow-Origin: *`). Those images load in a normal browser. `referrerpolicy="no-referrer"` plus an `onerror` fallback to the local SVG covers hotlink blocks.

AP / Reuters / Getty 2026 news stills are **not** copied. Each story footer and caption links the originating article or photo gallery.

| Local file | Role |
|---|---|
| diesel-pump.svg / diesel-chart.svg | Local fallback for energy stories |
| ceuta-coast.svg / ceuta-chart.svg | Local fallback for Ceuta |
| plane-lake.svg | Local fallback for Wausau landing |
| fema-field.svg | Local fallback for FEMA |
| ai-cluster.svg | Local fallback for AI |
| ireland-farmleigh.svg | Local fallback for Farmleigh |
| day-banner.svg | Masthead |

Remote originals used on story pages:
- FEMA PD: https://commons.wikimedia.org/wiki/File:FEMA_-_33673_-_Photograph_by_Patsy_Lynch_taken_on_09-24-2005_in_Louisiana.jpg
- Ceuta border: https://commons.wikimedia.org/wiki/File:Spanish-Moroccan_border_(Ceuta-Sebta).JPG
- Farmleigh: https://commons.wikimedia.org/wiki/File:Farmleigh,_Dublin.JPG
- Ceuta 2026 AP gallery (not copied): https://apnews.com/photo-gallery/migrants-cross-spain-s-ceuta-enclave-morocco-photos-b243d8b2df1d40b6a68a7958113d1ffd
- BLS tables: https://www.bls.gov/news.release/cpi.nr0.htm
