# `osmchange` to create OSM objects

Prepare data to create OSM objects.

## Usage

``` r
osmchange_create(x, format = c("R", "osc", "xml"))
```

## Arguments

- x:

  A
  [osmapi_objects](https://docs.ropensci.org/osmapiR/reference/osmapi_objects.md)
  with columns `type`, `changeset` + column `members` for ways and
  relations + `lat` and `lon` for nodes + tags if needed.

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

Objects IDs are unknown and will be allocated by the server. If `id`
column is missing in `x`, a negative placeholders will be used. Check
[OsmChange page](https://wiki.openstreetmap.org/wiki/OsmChange) for
details about how to refer to objects still not created to define the
members of relations and nodes of ways.

## See also

Other OsmChange's functions:
[`osm_diff_upload_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_diff_upload_changeset.md),
[`osm_download_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_download_changeset.md),
[`osmchange_delete()`](https://docs.ropensci.org/osmapiR/reference/osmchange_delete.md),
[`osmchange_modify()`](https://docs.ropensci.org/osmapiR/reference/osmchange_modify.md)

## Examples

``` r
d <- data.frame(
  type = c("node", "node", "way", "relation"),
  id = -(1:4),
  lat = c(0, 1, NA, NA),
  lon = c(0, 1, NA, NA),
  name = c(NA, NA, "My way", "Our relation"),
  type.1 = c(NA, NA, NA, "Column clash!")
)
d$members <- list(
  NULL, NULL, -(1:2),
  matrix(
    c("node", "-1", NA, "node", "-2", NA, "way", "-3", "outer"),
    nrow = 3, ncol = 3, byrow = TRUE, dimnames = list(NULL, c("type", "ref", "role"))
  )
)
obj <- osmapi_objects(d, tag_columns = c(name = "name", type = "type.1"))
osmcha <- osmchange_create(obj)
osmcha
#>   action_type     type id  lat  lon
#> 1      create     node -1    0    0
#> 2      create     node -2    1    1
#> 3      create      way -3 <NA> <NA>
#> 4      create relation -4 <NA> <NA>
#>                                           members
#> 1                                            NULL
#> 2                                            NULL
#> 3                                 2 nodes: -1, -2
#> 4 3 members: node/-1/NA, node/-2/NA, way/-3/outer
#>                                             tags
#> 1                                        No tags
#> 2                                        No tags
#> 3                             1 tag: name=My way
#> 4 2 tags: name=Our relation | type=Column clash!
```
