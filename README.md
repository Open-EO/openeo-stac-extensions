# openeo-stac-extensions
Key-values within STAC Extensions specific to openEO

## Datacube Extensions

### Horizontal Spatial Dimensions Object

- reference_system object with `"id":{"authority":"OGC","version":"1.3","code":"Auto42001"}`: Deepending on the location a different default crs (in this case the corresponding UTM zone) is used. For more info see `urn:ogc:def:crs:OGC:1.3:AUTO42001:99:8888` definded by OGC ([Definition identifier URNs in OGC namespace](https://portal.ogc.org/files/?artifact_id=24045))

## Electro-Optical Extension 

### eo:bands

| Field name | Value | Description |
| -----------|-------|-------------|
| openeo:gsd | [GSD Object](#GSD-Object)| An array containing GSD value and unit. |

### GSD Object

| Field name | Value | Description |
| -----------|----------|-------------|
| value      | [number] | **REQUIRED.** Collection's default pixel spacing in [x/y] direction in the unit of the reference_system specified in the datacube extension. Conversion factor between m and degrre (111 km = 1°) |
| unit       | m/°    | **REQUIRED.** Specifies the unit of the value field within the GSD object. |

*For sar and non optical data openeo:gsd is placed within `raster:bands`.