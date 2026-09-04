# Create an OSM object

Creates a new element in an open changeset as specified.

## Usage

``` r
osm_create_object(x, changeset_id)
```

## Arguments

- x:

  The new object data. Can be the path to an xml file, a
  [xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) or a
  data.frame inheriting or following the structure of an
  `osmapi_objects` object.

- changeset_id:

  The ID of an open changeset where to create the object. If missing,
  `x` should define the changeset ID, otherwise it will be overwritten
  with `changeset_id`. Ignored if `x` is a path.

## Value

The ID of the newly created OSM object.

## Details

If `x` is a data.frame, the columns `type`, `changeset`, `tags` must be
present + column `members` for ways and relations + `lat` and `lon` for
nodes. For the xml format, see the [OSM
wiki](https://wiki.openstreetmap.org/wiki/API_v0.6#Create:_PUT_/api/0.6/%5Bnode%7Cway%7Crelation%5D/create).

If multiple elements are provided only the first is created. The rest is
discarded.

## Note

- This updates the bounding box of the changeset.

- The `role` attribute for relations is optional. An empty string is the
  default.

- To avoid performance issues when uploading multiple objects, the use
  of the
  [`osm_diff_upload_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_diff_upload_changeset.md)
  is highly recommended.

- The version of the created object will be 1.

## See also

Other edit OSM objects' functions:
[`osm_delete_object()`](https://docs.ropensci.org/osmapiR/reference/osm_delete_object.md),
[`osm_update_object()`](https://docs.ropensci.org/osmapiR/reference/osm_update_object.md)

## Examples

``` r
vignette("how_to_edit_osm", package = "osmapiR")
#> Warning: vignette ‘how_to_edit_osm’ not found
```
