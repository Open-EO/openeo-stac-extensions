# openeo-stac-extensions

Additional fields for STAC used within openEO and other details about how existing STAC extensions are used in openEO.

## Links

### Links to WMTS services

To add a OGC WMTS service as a link to a resource for visualization, a new link `rel` type has been defined for the STAC [Link Object](https://github.com/radiantearth/stac-spec/tree/master/item-spec/item-spec.md#link-object).

| Type | Description |
| ------------------- | ----------- |
| wmts | This link points to a WMTS service, without query parameters. |

Additional fields that can be used in the Link object if the `rel` type has been set to `wmts`:

| Field name      | Data Type         | Description |
| --------------- | ----------------- | ----------- |
| wmts:layer      | string\|\[string] | A single layer as string or a list of layers as array of strings. All layers should be added/visualized on the map. |
| wmts:dimensions | Map<string, \*>   | Dimension information to be added as query parameters to the link. The key is the query parameter name, the value is the query parameter value. |

Example:

```json
{
	"href": "https://services.terrascope.be/wmts/v2",
	"rel": "wmts",
	"title": "WMTS for TERRASCOPE_S2_FAPAR_V2",
	"wmts:layer": "CGS_S2_FAPAR",
	"wmts:dimensions": {
		"time": "2015-12-31"
	}
}
```

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
