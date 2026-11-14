# `osmchange` to modify existing OSM objects

Prepare data to update tags, members and/or latitude and longitude.

## Usage

``` r
osmchange_modify(
  x,
  tag_keys,
  members = FALSE,
  lat_lon = FALSE,
  format = c("R", "osc", "xml")
)
```

## Arguments

- x:

  A
  [osmapi_objects](https://docs.ropensci.org/osmapiR/reference/osmapi_objects.md)
  with the columns `type` and `id` with unique combinations of values
  plus columns specifying tags, members or latitude and longitude.

- tag_keys:

  A character vector with the keys of the tags that will be modified. If
  missing (default), all tags will be updated, removed or created. If
  `FALSE`, don't modify tags.

- members:

  If `TRUE` and `x` has a `members` column, update the members of the
  ways and relations objects.

- lat_lon:

  If `TRUE` and `x` has a `lat` and `lon` columns, update the
  coordinates of the node objects.

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

`x` should be a `osmapi_objects` or follow the same format. Missing tags
or tags with `NA` in the value will be removed if `tag_keys` is not
specified. See
[`osm_get_objects()`](https://docs.ropensci.org/osmapiR/reference/osm_get_objects.md)
for examples of the format.

## See also

Other OsmChange's functions:
[`osm_diff_upload_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_diff_upload_changeset.md),
[`osm_download_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_download_changeset.md),
[`osmchange_create()`](https://docs.ropensci.org/osmapiR/reference/osmchange_create.md),
[`osmchange_delete()`](https://docs.ropensci.org/osmapiR/reference/osmchange_delete.md)

## Examples

``` r
obj <- osm_get_objects(
  osm_type = c("node", "way", "way", "relation", "relation", "node"),
  osm_id = c("35308286", "13073736", "235744929", "40581", "341530", "1935675367"),
  version = c(1, 3, 2, 5, 7, 1) # Old versions
)
osmch <- osmchange_modify(obj)
osmch
#>   action_type     type         id visible version changeset           timestamp
#> 1      modify     node   35308286    TRUE      17 140341361 2023-08-24 20:19:22
#> 2      modify      way   13073736    TRUE      29 158012506 2024-10-17 14:56:13
#> 3      modify      way  235744929    TRUE       8 157827160 2024-10-13 09:56:01
#> 4      modify relation      40581    TRUE      75 188255118 2026-08-30 15:35:18
#> 5      modify relation     341530    TRUE      26 181984197 2026-04-29 11:46:29
#> 6      modify     node 1935675367    TRUE      13 113921323 2021-11-17 23:47:45
#>                user      uid        lat        lon
#> 1          jmaspons 11725140 42.5189047  2.4565596
#> 2    homocomputeris  3777620       <NA>       <NA>
#> 3          pantufla  9104166       <NA>       <NA>
#> 4      davide020382 24247338       <NA>       <NA>
#> 5 Hugoren Martinako  3392826       <NA>       <NA>
#> 6          Jordi MF  8278438 38.8326220 -0.4063146
#>                                                           members
#> 1                                                            NULL
#> 2 61 nodes: 6771540804, 6771540805, 6771540806, 6957604952, 67...
#> 3 5 nodes: 2438033107, 2438033109, 2992282983, 2992282984, 243...
#> 4 57 members: node/72994199/admin_centre, way/1356521052/outer...
#> 5 17 members: node/359920433/admin_centre, way/45324328/outer,...
#> 6                                                            NULL
#>                                                                                  tags
#> 1 5 tags: altitude=2784,66 | created_by=Potlatch alpha | ele=2784,66 | name=Pic du...
#> 2                      3 tags: building=tower | historic=tower | name=Torres de Quart
#> 3 4 tags: barrier=wall | historic=memorial | name=Fossar de les Moreres | wikipedi...
#> 4 7 tags: admin_level=8 | boundary=administrative | name=Alghero | ref:catasto=A19...
#> 5 17 tags: admin_level=8 | boundary=administrative | idee:name=Fraga | ine:municip...
#> 6                                                  2 tags: ele=1104 | name=Benicadell
```
