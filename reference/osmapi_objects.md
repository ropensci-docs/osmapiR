# osmapi_objects constructor

osmapi_objects constructor

## Usage

``` r
osmapi_objects(x, tag_columns, keep_na_tags = FALSE)
```

## Arguments

- x:

  `data.frame` representing OSM objects as rows. At least it has a
  `type` column with `node`, `way` or `relation`.

- tag_columns:

  A vector indicating the name or position of the columns representing
  tags. If missing, it's assumed that `tags` column contain the tags
  (see details).

- keep_na_tags:

  If `TRUE`, don't drop the empty tags specified in `tag_columns` and
  add `NA` as a value. Useful to remove specific tags with
  [`osmchange_modify()`](https://docs.ropensci.org/osmapiR/reference/osmchange_modify.md)
  and specific `tag_keys`.

## Value

An `osmapi_objects`

## See also

Other get OSM objects' functions:
[`osm_bbox_objects()`](https://docs.ropensci.org/osmapiR/reference/osm_bbox_objects.md),
[`osm_get_objects()`](https://docs.ropensci.org/osmapiR/reference/osm_get_objects.md),
[`osm_history_object()`](https://docs.ropensci.org/osmapiR/reference/osm_history_object.md),
[`osm_relations_object()`](https://docs.ropensci.org/osmapiR/reference/osm_relations_object.md),
[`osm_ways_node()`](https://docs.ropensci.org/osmapiR/reference/osm_ways_node.md)

## Examples

``` r
x <- data.frame(
  type = c("node", "node", "way"), id = 1:3, name = c(NA, NA, "My way")
)
x$members <- list(NULL, NULL, 1:2)
obj <- osmapi_objects(x, tag_columns = "name")
obj
#>   type id       members               tags
#> 1 node  1          NULL            No tags
#> 2 node  2          NULL            No tags
#> 3  way  3 2 nodes: 1, 2 1 tag: name=My way
```
