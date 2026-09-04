# Ways of a node

Returns all the (not deleted) ways in which the given node is used.

## Usage

``` r
osm_ways_node(node_id, format = c("R", "xml", "json"), tags_in_columns = FALSE)
```

## Arguments

- node_id:

  Node id represented by a numeric or a character value.

- format:

  Format of the output. Can be `"R"` (default), `"xml"`, or `"json"`.

- tags_in_columns:

  If `FALSE` (default), the tags of the objects are saved in a single
  list column `tags` containing a `data.frame` for each OSM object with
  the keys and values. If `TRUE`, add a column for each key. Ignored if
  `format != "R"`.

## Value

If `format = "R"`, returns a data frame with one OSM object per row. If
`format = "xml"`, returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md)
following the [OSM_XML
format](https://wiki.openstreetmap.org/wiki/OSM_XML#OSM_XML_file_format_notes).
If `format = "json"`, returns a list with a json structure following the
[OSM_JSON format](https://wiki.openstreetmap.org/wiki/OSM_JSON).

## See also

Other get OSM objects' functions:
[`osm_bbox_objects()`](https://docs.ropensci.org/osmapiR/reference/osm_bbox_objects.md),
[`osm_get_objects()`](https://docs.ropensci.org/osmapiR/reference/osm_get_objects.md),
[`osm_history_object()`](https://docs.ropensci.org/osmapiR/reference/osm_history_object.md),
[`osm_relations_object()`](https://docs.ropensci.org/osmapiR/reference/osm_relations_object.md),
[`osmapi_objects()`](https://docs.ropensci.org/osmapiR/reference/osmapi_objects.md)

## Examples

``` r
ways_node <- osm_ways_node(node_id = 35308286)
ways_node
#>   type        id visible version changeset           timestamp        user
#> 1  way 215647946    TRUE       2  15632492 2013-04-06 21:14:46      Pinpin
#> 2  way 242517580    TRUE       9 181111809 2026-04-09 18:16:58 Imain 🐿🥾🥾
#> 3  way 656589709    TRUE       2 113253385 2021-11-01 20:20:52    jmaspons
#>        uid  lat  lon
#> 1     1685 <NA> <NA>
#> 2  3498572 <NA> <NA>
#> 3 11725140 <NA> <NA>
#>                                                           members
#> 1 7 nodes: 940255814, 940255832, 940255835, 940255464, 3530828...
#> 2 238 nodes: 35308286, 1853967143, 302096532, 302096535, 52262...
#> 3 26 nodes: 877753155, 877753159, 877753191, 877753195, 877753...
#>                                                                                  tags
#> 1 3 tags: admin_level=8 | boundary=administrative | source=cadastre-dgi-fr source ...
#> 2 5 tags: highway=path | sac_scale=mountain_hiking | surface=gravel | trail_visibi...
#> 3                       3 tags: highway=path | sac_scale=alpine_hiking | surface=rock
```
