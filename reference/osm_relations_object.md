# Relations of an object

Returns all (not deleted) relations in which the given object is used.

## Usage

``` r
osm_relations_object(
  osm_type = c("node", "way", "relation"),
  osm_id,
  format = c("R", "xml", "json"),
  tags_in_columns = FALSE
)
```

## Arguments

- osm_type:

  Object type (`"node"`, `"way"` or `"relation"`).

- osm_id:

  Object id represented by a numeric or a character value.

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
[`osm_ways_node()`](https://docs.ropensci.org/osmapiR/reference/osm_ways_node.md),
[`osmapi_objects()`](https://docs.ropensci.org/osmapiR/reference/osmapi_objects.md)

## Examples

``` r
node <- osm_relations_object(osm_type = "node", osm_id = 152364165)
node
#>       type       id visible version changeset           timestamp
#> 1 relation   347950    TRUE     124 188066001 2026-08-26 20:26:30
#> 2 relation   349035    TRUE     177 179308493 2026-03-03 15:42:08
#> 3 relation   349053    TRUE     826 186576884 2026-07-29 10:53:23
#> 4 relation  2417889    TRUE      66 186723166 2026-07-31 18:31:18
#> 5 relation  2807397    TRUE     118 181248091 2026-04-12 20:14:10
#> 6 relation 11746917    TRUE     247 186576884 2026-07-29 10:53:23
#> 7 relation 11747082    TRUE     472 188207626 2026-08-29 16:53:14
#> 8 relation 21290432    TRUE       8 188269486 2026-08-30 20:04:12
#>               user      uid  lat  lon
#> 1 marcmarti_import 23854535 <NA> <NA>
#> 2      Yan Bakhmat 12495047 <NA> <NA>
#> 3           EliziR   605366 <NA> <NA>
#> 4      geoccitania 17533098 <NA> <NA>
#> 5         ivanruiz 23829548 <NA> <NA>
#> 6           EliziR   605366 <NA> <NA>
#> 7       Gorjablanc 21189916 <NA> <NA>
#> 8          Rico557  3281808 <NA> <NA>
#>                                                           members
#> 1 151 members: node/152364165/admin_centre, relation/3765380/s...
#> 2 532 members: node/152364165/admin_centre, way/45319680/outer...
#> 3 2265 members: way/1415938360/outer, way/83094965/outer, way/...
#> 4 115 members: node/152364165/admin_centre, way/185724656/oute...
#> 5 466 members: node/152364165/admin_centre, way/45327666/outer...
#> 6 2238 members: node/152364165/admin_centre, way/585618147/out...
#> 7 3760 members: node/8000963558/label, node/152364165/admin_ce...
#> 8 3623 members: node/8000963558/label, node/152364165/admin_ce...
#>                                                                                  tags
#> 1   39 tags: admin_level=8 | alt_name:gl=Barna | alt_name:hi=बार्सेलोना | border_typ...
#> 2 36 tags: admin_level=6 | alt_name:br=Barselona | boundary=administrative | ine:p...
#> 3 71 tags: admin_level=4 | alt_name:el=Καταλονία | alt_name:eo=Katalunujo | alt_na...
#> 4 26 tags: admin_level=7 | border_type=comarca | boundary=administrative | name=Ba...
#> 5 8 tags: boundary=political | idescat:àmbit=01 | name=Àmbit metropolità de Barcel...
#> 6 11 tags: boundary=political | default_language=ca | name=Català com a llengua pr...
#> 7 49 tags: boundary=political | name=Països Catalans | name:an=Países Catalans | n...
#> 8 8 tags: boundary=civil | name=Domini lingüístic català | name:be=Каталанска-моўн...

way <- osm_relations_object(osm_type = "way", osm_id = 372011578)
way
#>       type      id visible version changeset           timestamp      user
#> 1 relation 5524720    TRUE      69 186886687 2026-08-03 18:58:17 MacLondon
#>      uid  lat  lon
#> 1 322039 <NA> <NA>
#>                                                           members
#> 1 206 members: relation/6959819/alternative, way/372006138/, w...
#>                                                                                  tags
#> 1 9 tags: distance=62.65 | name=Sender dels Maquis | network=nwn | operator=GR | o...

rel <- osm_relations_object(osm_type = "relation", osm_id = 342792)
rel
#>       type       id visible version changeset           timestamp       user
#> 1 relation   349012    TRUE     138 188186993 2026-08-29 09:32:21 Gorjablanc
#> 2 relation 11739086    TRUE     120 187294867 2026-08-11 16:05:26    flierfy
#>        uid  lat  lon
#> 1 21189916 <NA> <NA>
#> 2   445671 <NA> <NA>
#>                                                           members
#> 1 497 members: node/21323935/admin_centre, way/1153082462/oute...
#> 2 1068 members: node/34105607/admin_centre, node/8000963555/la...
#>                                                                                  tags
#> 1 35 tags: admin_level=6 | alt_name:gl=Alacante | border_type=province | boundary=...
#> 2 53 tags: boundary=political | default_language=ca | name=Municipis de Predomini ...
```
