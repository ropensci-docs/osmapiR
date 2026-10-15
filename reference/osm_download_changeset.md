# Download a changeset in `OsmChange` format

Returns the [OsmChange](https://wiki.openstreetmap.org/wiki/OsmChange)
document describing all changes associated with the changeset.

## Usage

``` r
osm_download_changeset(changeset_id, format = c("R", "osc", "xml"))
```

## Arguments

- changeset_id:

  The id of the changeset represented by a numeric or a character value
  for which the OsmChange is requested.

- format:

  Format of the output. Can be `"R"` (default) or `"osc"` (`"xml"` is a
  synonym for `"osc"`).

## Value

If `format = "R"`, returns a data frame with one row for each edit
action in the changeset. If `format = "osc"`, returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) in the
[OsmChange](https://wiki.openstreetmap.org/wiki/OsmChange) format.

## Details

- The result of calling this may change as long as the changeset is
  open.

- The elements in the OsmChange are sorted by timestamp and version
  number.

- There is
  [`osm_get_changesets()`](https://docs.ropensci.org/osmapiR/reference/osm_get_changesets.md)
  to get only information about the changeset itself.

## See also

Other get changesets' functions:
[`osm_get_changesets()`](https://docs.ropensci.org/osmapiR/reference/osm_get_changesets.md),
[`osm_query_changesets()`](https://docs.ropensci.org/osmapiR/reference/osm_query_changesets.md)

Other OsmChange's functions:
[`osm_diff_upload_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_diff_upload_changeset.md),
[`osmchange_create()`](https://docs.ropensci.org/osmapiR/reference/osmchange_create.md),
[`osmchange_delete()`](https://docs.ropensci.org/osmapiR/reference/osmchange_delete.md),
[`osmchange_modify()`](https://docs.ropensci.org/osmapiR/reference/osmchange_modify.md)

## Examples

``` r
chaset <- osm_download_changeset(changeset_id = 137003062)
chaset
#>    action_type type          id visible version changeset           timestamp
#> 1       create node 10959104783    TRUE       1 137003062 2023-06-06 08:18:47
#> 2       create node 10959104784    TRUE       1 137003062 2023-06-06 08:18:47
#> 3       create node 10959104785    TRUE       1 137003062 2023-06-06 08:18:47
#> 4       create node 10959104786    TRUE       1 137003062 2023-06-06 08:18:47
#> 5       create node 10959104787    TRUE       1 137003062 2023-06-06 08:18:47
#> 6       create node 10959104788    TRUE       1 137003062 2023-06-06 08:18:47
#> 7       create  way  1179939727    TRUE       1 137003062 2023-06-06 08:18:47
#> 8       create  way  1179939728    TRUE       1 137003062 2023-06-06 08:18:47
#> 9       modify node   472315639    TRUE       3 137003062 2023-06-06 08:18:47
#> 10      modify  way   144018965    TRUE       6 137003062 2023-06-06 08:18:47
#> 11      modify  way   772922459    TRUE       8 137003062 2023-06-06 08:18:47
#> 12      modify  way    39428288    TRUE      11 137003062 2023-06-06 08:18:47
#> 13      modify  way   144017967    TRUE      11 137003062 2023-06-06 08:18:47
#>        user     uid        lat        lon
#> 1  MariaDCC 7951616 39.9312656 -0.0611038
#> 2  MariaDCC 7951616 39.9275936 -0.0633938
#> 3  MariaDCC 7951616 39.9186918 -0.0668522
#> 4  MariaDCC 7951616 39.9186426 -0.0669390
#> 5  MariaDCC 7951616 39.9143313 -0.0585758
#> 6  MariaDCC 7951616 39.9275524 -0.0556357
#> 7  MariaDCC 7951616       <NA>       <NA>
#> 8  MariaDCC 7951616       <NA>       <NA>
#> 9  MariaDCC 7951616 39.9144031 -0.0632470
#> 10 MariaDCC 7951616       <NA>       <NA>
#> 11 MariaDCC 7951616       <NA>       <NA>
#> 12 MariaDCC 7951616       <NA>       <NA>
#> 13 MariaDCC 7951616       <NA>       <NA>
#>                                                            members
#> 1                                                             NULL
#> 2                                                             NULL
#> 3                                                             NULL
#> 4                                                             NULL
#> 5                                                             NULL
#> 6                                                             NULL
#> 7  5 nodes: 10959104783, 1579678230, 8701431676, 8701431680, 10...
#> 8  101 nodes: 1579678230, 1579678224, 8701431674, 1579678222, 1...
#> 9                                                             NULL
#> 10                    3 nodes: 1575984666, 10959104783, 1575984667
#> 11 20 nodes: 472315862, 472315695, 8705264405, 472315697, 47231...
#> 12 71 nodes: 6207335786, 6207335788, 6207335787, 472315576, 472...
#> 13 97 nodes: 1579678210, 1579678208, 1579678203, 8701431694, 15...
#>                                                                                   tags
#> 1                                                                              No tags
#> 2                                                                              No tags
#> 3                                                                              No tags
#> 4                                                                              No tags
#> 5                                                                              No tags
#> 6                                                                              No tags
#> 7                                                               1 tag: landuse=orchard
#> 8                                                               1 tag: landuse=orchard
#> 9                                                                              No tags
#> 10 6 tags: bridge=yes | highway=cycleway | layer=1 | lit=no | ref=CR-18 | surface=a...
#> 11 6 tags: highway=unclassified | lane_markings=no | name=Camí de La Cantera de Vor...
#> 12 4 tags: highway=unclassified | name=Camí dels Carnissers | name:ca=Camí dels Car...
#> 13                         3 tags: highway=unclassified | noname=yes | surface=asphalt
```
