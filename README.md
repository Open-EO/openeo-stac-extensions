# openeo-stac-extensions

Additional fields for STAC used within openEO and other details about how existing STAC extensions are used in openEO.

## Datacube Extensions

### Horizontal Spatial Dimensions Object

- `reference_system` object with `"id":{"authority":"OGC","version":"1.3","code":"Auto42001"}`: Deepending on the location a different default crs (in this case the corresponding UTM zone) is used. For more info see `urn:ogc:def:crs:OGC:1.3:AUTO42001:99:8888` definded by OGC ([Definition identifier URNs in OGC namespace](https://portal.ogc.org/files/?artifact_id=24045))

## Electro-Optical / Raster Extension 

### eo:bands / raster:bands

| Field name | Data Type | Description |
| ---------- | --------- | ----------- |
| openeo:gsd | [GSD Object](#GSD-Object) | An array containing GSD value and unit. |

* For EO data the field is added to `eo:bands` entries.
* For SAR and non-optical data the field is added to `raster:bands` entries.

#### GSD Object

| Field name | Data Type | Description |
| ---------- | --------- | ----------- |
| value      | \[number] | **REQUIRED.** Collection's default pixel spacing in [x/y] direction in the unit of the reference_system specified in the datacube extension. Conversion factor between m and degrre (111 km = 1°) |
| unit       | string    | **REQUIRED.** Specifies the unit of the value field within the GSD object. One of `m` (meters) or `°` (degrees). |

## Data Processing

For Items and Collections provided as batch job results:

| Field name    | Data Type | Description |
| ------------- | --------- | ----------- |
| openeo:status | string    | Indicates the status of the underlying batch job processing, must be one of `running`, `canceled`, `finished`, `error`. For example, this can be used to indicate whether a STAC resource is complete (`finished`) or Potentially incomplete (all other states). |

## Collection filtering

| Field name              | Data Type | Description |
| ----------------------- | --------- | ----------- |
| openeo:property_filters | \[string] | Gives a list of properties you can filter on when loading data from the collection. Returning an empty array means that no property-based filters are available. This is a guide for users to get an overview of available properties to filter on. More metadata about the properties can be found in `summaries`. |

## Links (Web Map Links)

Links to WMTS and XYZ services can be provided through the [Web Map Links](https://github.com/stac-extensions/web-map-links) extension.
Initially defined within the openEO platform project for openEO, but has been split apart into a separate extension which is fully compliant to what is used in openEO.
