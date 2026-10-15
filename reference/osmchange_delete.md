# `osmchange` to delete existing OSM objects

Prepare data to delete OSM objects.

## Usage

``` r
osmchange_delete(x, delete_if_unused = FALSE, format = c("R", "osc", "xml"))
```

## Arguments

- x:

  A
  [osmapi_objects](https://docs.ropensci.org/osmapiR/reference/osmapi_objects.md)
  or `data.frame` with the columns `type` and `id` for the objects to
  delete. Other columns will be ignored.

- delete_if_unused:

  If `TRUE`, the `if-unused` attribute will be added (see details). Can
  be a vector of length `nrow(x)`.

- format:

  Format of the output. Can be `"R"` (default), `"osc"` (`"xml"` is a
  synonym for `"osc"`).

## Value

If `format = "R"`, returns a `osmapi_OsmChange` data frame with one OSM
edition per row. If `format = "osc"` or `format = "xml"`, returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md)
following the [OsmChange
format](https://wiki.openstreetmap.org/wiki/OsmChange) that can be saved
with [`xml2::write_xml()`](http://xml2.r-lib.org/reference/write_xml.md)
and opened in other applications such as JOSM.

The results are ready to send the editions to the servers with
[`osm_diff_upload_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_diff_upload_changeset.md).

## Details

If `if-unused` attribute is present, then the delete operation(s) in
this block are conditional and will only be executed if the object to be
deleted is not used by another object. Without the `if-unused`, such a
situation would lead to an error, and the whole diff upload would fail.
Setting the attribute will also cause deletions of already deleted
objects to not generate an error.

## See also

Other OsmChange's functions:
[`osm_diff_upload_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_diff_upload_changeset.md),
[`osm_download_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_download_changeset.md),
[`osmchange_create()`](https://docs.ropensci.org/osmapiR/reference/osmchange_create.md),
[`osmchange_modify()`](https://docs.ropensci.org/osmapiR/reference/osmchange_modify.md)

## Examples

``` r
obj_id <- osmapi_objects(data.frame(
  type = c("way", "way", "relation", "node"),
  id = c("722379703", "629132242", "8387952", "4739010921")
))
osmchange_del <- osmchange_delete(obj_id)
```
