# Get OSM objects

Retrieve objects by `type`, `id` and `version`.

## Usage

``` r
osm_get_objects(
  osm_type,
  osm_id,
  version,
  full_objects = FALSE,
  format = c("R", "xml", "json"),
  tags_in_columns = FALSE
)
```

## Arguments

- osm_type:

  A vector with the type of the objects (`"node"`, `"way"` or
  `"relation"`). Recycled if it has a different length than `osm_id`.

- osm_id:

  Object ids represented by a numeric or a character vector.

- version:

  An optional vector with the version number for each object. If
  missing, the last version will be retrieved. Recycled if it has
  different length than `osm_id`.

- full_objects:

  If `TRUE`, retrieves all other objects referenced by ways or
  relations. Not compatible with `version`.

- format:

  Format of the output. Can be `"R"` (default), `"xml"`, or `"json"`.

- tags_in_columns:

  If `FALSE` (default), the tags of the objects are saved in a single
  list column
  ```` tags``` containing a  ````data.frame`for each OSM object with the keys and values. If`TRUE`, add a column for each key. Ignored if `format
  != "R"\`.

## Value

If `format = "R"`, returns a data frame with one OSM object per row. If
`format = "xml"`, returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md)
following the [OSM_XML
format](https://wiki.openstreetmap.org/wiki/OSM_XML#OSM_XML_file_format_notes).
If `format = "json"`, returns a list with a json structure following the
[OSM_JSON format](https://wiki.openstreetmap.org/wiki/OSM_JSON).

Objects are sorted in the same order than `osm_id` except for
`full_objects = TRUE`, where the nodes comes first, then ways, and
relations at the end as specified by [OSM_XML
format](https://wiki.openstreetmap.org/wiki/OSM_XML#OSM_XML_file_format_notes).

## Details

`full_objects = TRUE` does not support specifying `version`. For ways,
`full_objects = TRUE` implies that it will return the way specified plus
all nodes referenced by the way. For a relation, it will return the
following:

- The relation itself

- All nodes, ways, and relations that are members of the relation

- Plus all nodes used by ways from the previous step

- The same recursive logic is not applied to relations. This means: If
  relation r1 contains way w1 and relation r2, and w1 contains nodes n1
  and n2, and r2 contains node n3, then a "full" request for r1 will
  give you r1, r2, w1, n1, and n2. Not n3.

## Note

For downloading data for purposes other than editing or exploring the
history of the objects, perhaps is better to use the Overpass API. A
similar function to download OSM objects by `type` and `id` using
Overpass, is implemented in the osmdata function `opq_osm_id()`.

## See also

Other get OSM objects' functions:
[`osm_bbox_objects()`](https://docs.ropensci.org/osmapiR/reference/osm_bbox_objects.md),
[`osm_history_object()`](https://docs.ropensci.org/osmapiR/reference/osm_history_object.md),
[`osm_relations_object()`](https://docs.ropensci.org/osmapiR/reference/osm_relations_object.md),
[`osm_ways_node()`](https://docs.ropensci.org/osmapiR/reference/osm_ways_node.md),
[`osmapi_objects()`](https://docs.ropensci.org/osmapiR/reference/osmapi_objects.md)

## Examples

``` r
obj <- osm_get_objects(
  osm_type = c("node", "way", "way", "relation", "relation", "node"),
  osm_id = c("35308286", "13073736", "235744929", "40581", "341530", "1935675367"),
  version = c(1, 3, 2, 5, 7, 1)
)
obj
#>       type         id visible version changeset           timestamp        user
#> 1     node   35308286    TRUE       1    292412 2007-09-02 14:55:33     Skywave
#> 2      way   13073736    TRUE       3   9724157 2011-11-02 17:55:59       morsi
#> 3      way  235744929    TRUE       2  18871484 2013-11-13 10:32:50         SMP
#> 4 relation      40581    TRUE       5  11839138 2012-06-08 20:25:11       lerks
#> 5 relation     341530    TRUE       7  44169637 2016-12-05 01:12:32     nyuriks
#> 6     node 1935675367    TRUE       1  13275996 2012-09-27 18:44:25 user_293845
#>      uid        lat        lon
#> 1  10927 42.5178841  2.4567366
#> 2 139580       <NA>       <NA>
#> 3  54441       <NA>       <NA>
#> 4 188477       <NA>       <NA>
#> 5 339581       <NA>       <NA>
#> 6 293845 38.8326988 -0.4065295
#>                                                           members
#> 1                                                            NULL
#> 2 17 nodes: 120303676, 120303671, 120303597, 120303605, 120303...
#> 3                                 2 nodes: 2438033107, 2438033109
#> 4 13 members: way/27966652/outer, way/27966846/outer, way/2796...
#> 5 17 members: way/45335182/outer, way/45324328/outer, way/4533...
#> 6                                                            NULL
#>                                                                                  tags
#> 1 5 tags: altitude=2784,66 | created_by=Potlatch alpha | ele=2784,66 | name=Pic du...
#> 2                      3 tags: building=tower | historic=tower | name=Torres de Quart
#> 3 4 tags: barrier=wall | historic=memorial | name=Fossar de les Moreres | wikipedi...
#> 4 7 tags: admin_level=8 | boundary=administrative | name=Alghero | ref:catasto=A19...
#> 5 17 tags: admin_level=8 | boundary=administrative | idee:name=Fraga | ine:municip...
#> 6                                                  2 tags: ele=1104 | name=Benicadell
```
