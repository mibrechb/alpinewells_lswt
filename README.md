# AlpLakes_LSWT

The temperature data in this repository consists of aggregated (median) Landsat ST (Collection 2, Level 2) data from 1982-08-22 to present (using L4, L5, L7, L8, L9) based on this [GEE script](https://code.earthengine.google.com/a0742a9bb6329d5925cc5ba7e4a1ce4a?noload=true). Alternatively, this [GEE script](https://code.earthengine.google.com/e5df6e79d2e54eb66e72e4bdab89222c) can be used to extract datapoints for a single lake (including hand drawn polygons) and inspect the associated RGB/TIR scenes.

## Data columns:
| Column            | Description                                           |
|:-------------     | -------------                                         |
| LANDSAT_SCENE_ID  | Short Landsat Scene Identifier                        |
| ST                | Aggregated ST (K)                                     |
| ST_CDIST          | Distance to cloud (km)                                |
| ST_QA             | Uncertainty of the Surface Temperature band (K) *     |
| coverage          | Percentage of unmasked lake area                      |
| px_count          | No. of unmasked pixels available for datapoint        |
| sensor            | Landsat sensor platform used (e.g. LANDSAT_9)         |
| time_utc          | Time of the observations as at center of scene in UTC |

* *The ST_QA values provide uncertainty values using a combination of uncertainty from a standard error propagation and distance to cloud. The method used is described in [Laraby et al. (2018)](https://doi.org/10.1016/j.rse.2018.06.026) for Landsat 7 but is also used in the entirety of Collection 2 ST products.*

## Used input parameters:

| Parameter               | Description                                                               | Value     |
|:-------------           |:-------------                                                             |:-----     |
| ROI_COVERAGE_THRESHOLD  | Treshold of unmasked ROI surface ranging from [0, 1]                      | 0.2       |
| UNCERTAINTY_TRESHOLD    | Treshold for uncertainty mask based on ST_QA band                         | 10        |
| CLOUD_COVER_TRESHOLD    | Treshold for cloud cover filter based on property 'CLOUD_COVER' [0, 100]  | 60        |
| start                   | Start date of timeseries as ee.Date('YYYY-MM-DD')                         | 1982-08-22|
| end                     | End date of timeseries as ee.Date('YYYY-MM-DD')                           | 2023-03-14|

## Used QA_PIXEL flags (CFMASK):
Landsat scenes are water- and cloud-masked with the following included [CFMASK](https://www.usgs.gov/landsat-missions/cfmask-algorithm) cloudflags:

| Bit No. | Description              | Used state |
|:--      |:------------------------ |:---------- |
| 1       | Dilated Cloud            | Off        |
| 3       | Cloud                    | Off        |
| 4       | Cloud Shadow             | Off        |
| 7       | Water                    | On (for *onlywater.zip) |


## EE datasets and documentations

Landsat Collection 2 Surface Tempearture general information  
https://www.usgs.gov/landsat-missions/landsat-collection-2-surface-temperature

Landsat 4: USGS Landsat 4 Level 2, Collection 2, Tier 1  
ee.ImageCollection('LANDSAT_LT04_C02_T1_L2')  
Documentation: https://developers.google.com/earth-engine/datasets/catalog/LANDSAT_LT04_C02_T1_L2

Landsat 5: USGS Landsat 5 Level 2, Collection 2, Tier 1  
ee.ImageCollection('LANDSAT/LT05/C02/T1_L2')  
Documentation: https://developers.google.com/earth-engine/datasets/catalog/LANDSAT_LT05_C02_T1_L2

Landsat 7: USGS Landsat 7 Level 2, Collection 2, Tier 1  
ee.ImageCollection('LANDSAT/LE07/C02/T1_L2')  
Documentation: https://developers.google.com/earth-engine/datasets/catalog/LANDSAT_LE07_C02_T1_L2

Landsat 8: USGS Landsat 8 Level 2, Collection 2, Tier 1  
ee.ImageCollection('LANDSAT/LC08/C02/T1_L2')  
Documentation: https://developers.google.com/earth-engine/datasets/catalog/LANDSAT_LC08_C02_T1_L2

Landsat 9: USGS Landsat 9 Level 2, Collection 2, Tier 1  
ee.ImageCollection('LANDSAT/LC09/C02/T1_L2')  
Documentation: https://developers.google.com/earth-engine/datasets/catalog/LANDSAT_LC09_C02_T1_L2
