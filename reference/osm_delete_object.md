# Delete an OSM object

Expects a valid XML representation of the element to be deleted.

## Usage

``` r
osm_delete_object(x, changeset_id)
```

## Arguments

- x:

  The object data. Can be the path of an xml file, a
  [xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) or a
  data.frame inheriting or following the structure of an
  `osmapi_objects` object.

- changeset_id:

  The ID of an open changeset where to create the object. If missing,
  `x` should define the changeset ID, otherwise it will be overwritten
  with `changeset_id`. Ignored if `x` is a path.

## Value

Returns the new version number of the object.

## Details

The version must match the version of the element you downloaded and the
changeset must match the `id` of an open changeset owned by the current
authenticated user. It is allowed, but not necessary, to have tags on
the element except for lat/lon which are required for nodes, without
lat+lon the server gives 400 Bad request.

If `x` is a data.frame, the columns `type`, `id`, `version` and
`changeset` must be present + `lat` and `lon` for nodes. For the xml
format, see the [OSM
wiki](https://wiki.openstreetmap.org/wiki/API_v0.6#Delete:_DELETE_/api/0.6/%5Bnode%7Cway%7Crelation%5D/%23id).

If multiple elements are provided only the first is deleted. The rest is
discarded.

## Note

- This updates the bounding box of the changeset.

- To avoid performance issues when deleting multiple objects, the use of
  the
  [`osm_diff_upload_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_diff_upload_changeset.md)
  is highly recommended. This is also the only way to ensure that
  multiple objects are updated in a single database transaction.

## See also

Other edit OSM objects' functions:
[`osm_create_object()`](https://docs.ropensci.org/osmapiR/reference/osm_create_object.md),
[`osm_update_object()`](https://docs.ropensci.org/osmapiR/reference/osm_update_object.md)

## Examples

``` r
vignette("how_to_edit_osm", package = "osmapiR")
#> Warning: vignette ‘how_to_edit_osm’ not found
```
