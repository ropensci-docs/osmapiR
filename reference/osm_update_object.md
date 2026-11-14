# Update an OSM object

Updates data from a preexisting element.

## Usage

``` r
osm_update_object(x, changeset_id)
```

## Arguments

- x:

  The new object data. Can be the path of an xml file, a
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

A full representation of the element as it should be after the update
has to be provided. Any tags, way-node refs, and relation members that
remain unchanged must be in the update as well. A version number must be
provided as well, it **must match** the current version of the element
in the database.

If `x` is a data.frame, the columns `type`, `id`, `visible`, `version`,
`changeset`, and `tags` must be present + column `members` for ways and
relations + `lat` and `lon` for nodes. For the xml format, see the [OSM
wiki](https://wiki.openstreetmap.org/wiki/API_v0.6#Update:_PUT_/api/0.6/%5Bnode%7Cway%7Crelation%5D/%23id).

If multiple elements are provided only the first is updated. The rest is
discarded.

## Note

- This updates the bounding box of the changeset.

- To avoid performance issues when updating multiple objects, the use of
  the
  [`osm_diff_upload_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_diff_upload_changeset.md)
  is highly recommended. This is also the only way to ensure that
  multiple objects are updated in a single database transaction.

  - If you can't use the
    [`osm_diff_upload_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_diff_upload_changeset.md)
    and plan to update more items, mind to do it sequentially (not in
    parallel).

## See also

Other edit OSM objects' functions:
[`osm_create_object()`](https://docs.ropensci.org/osmapiR/reference/osm_create_object.md),
[`osm_delete_object()`](https://docs.ropensci.org/osmapiR/reference/osm_delete_object.md)

## Examples

``` r
vignette("how_to_edit_osm", package = "osmapiR")
#> Warning: vignette ‘how_to_edit_osm’ not found
```
