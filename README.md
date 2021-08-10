
# the tu3djson formal specification


## What is tu3djson?

It stands for TU Delft 3D JSON specification, named after the [TU Delft 3D research group](https://3d.bk.tudelft.nl).
It is meant as a simple format to store/exchange 3D features since [GeoJSON](https://geojson.org/) is restricted to 2D primitives stored in WGS84 (even if the elevation with respect to the WGS84 ellipsoid can be stored, it is only 2.5D and not 3D).


## An example

```json
{
  "type": "tu3djson",
  "crs": "https://www.opengis.net/def/crs/EPSG/0/7415",
  "features": [
    {
      "type": "Building",
      "geometry": {
        "type": "MultiSurface",
        "boundaries": [
          [[0, 3, 2, 1]], [[4, 5, 6, 7]], [[0, 1, 5, 4]]
        ],
        "vertices": [
          [0.0, 0.0, 0.0],
          [1.0, 0.0, 0.0],
          [0.0, 0.0, 0.0]
        ]
      },
      "properties": {
        "name": "big rock"
      }
    },
    {
      "type": "Tree",
      "geometry": {
        "type": "Solid",
        "boundaries": [
          [ [[0, 3, 2, 1]], [[4, 5, 6, 7]], [[0, 1, 5, 4]] ]
        ],
        "vertices": [
          [0.0, 0.0, 0.0],
          [1.0, 0.0, 0.0],
          [0.0, 0.0, 0.0]
        ]
      },
      "properties": {
        "name": "another rock",
        "colour": "bright red"
      }
    }
  ]
}
```


## tu3djson object


A tu3djson object is a single JSON object containing zero or more Feature Objects.
It:

  - **must** have one member with the name `"type"`, whose value must be `"tu3djson"`.
  - **must** have one member with the name `"features"`, whose value is an array containing 0 or more Feature Objects
  - **may** have a member with the name `"crs"` (coordinate reference system), whose value is a URL formatted according to the [OGC Name Type Specification](https://docs.opengeospatial.org/pol/09-048r5.html#_production_rule_for_specification_element_names). All Features in the tu3djson object must be geo-referenced according to this CRS.


### Feature object

  - **must** have one member with the name `"type"`, whose value must be a string. The values of the type is not prescribed and should be used to describe the Feature Object. `"type": "Feature` is an acceptable property/value.
  - **must** have one member with the name `"geometry"`, whose value must be one Geometry Object.
  - **may** have one member with the name `"properties"`,  whose value is a JSON object.


### Geometry object


  - **must** have one member with the name `"type"`, whose value must be either:
    - `"MultiPoint"`
    - `"MultiLine"`
    - `"MultiSurface"`
    - `"CompositeSurface"`
    - `"Solid"`
    - `"MultiSolid"`
    - `"CompositeSolid"`
  - **must** have one member with the name `"boundaries"`
  - **must** have one member with the name `"vertices"`, whose value is an array of coordinates of each vertex of the current Geometry object. Their position in this array (0-based) is used to represent the Geometry Object.
  - **must** have one member with the name `"vertices"`, whose value is an array of coordinates of each vertex of the current Geometry Object, stored with integers. Their position in this array (0-based) is used as an index to be referenced by `"boundaries"` of the Geometry Object.


