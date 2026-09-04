# Change `tags` from a list column \<-\> columns for each key in wide format

Objects of classes `osmapi_objects` and `osmapi_changesets` can
represent the tags in a column with a list with a data.frame for each
row with 2 columns for keys and values, or by columns for each key.
These functions allow to change the format of the tags.

## Usage

``` r
tags_list2wide(x)

tags_wide2list(x)
```

## Arguments

- x:

  An `osmapi_objects` or `osmapi_changesets` objects as returned by, for
  example,
  [`osm_get_objects()`](https://docs.ropensci.org/osmapiR/reference/osm_get_objects.md)
  or
  [`osm_get_changesets()`](https://docs.ropensci.org/osmapiR/reference/osm_get_changesets.md).

## Value

A data frame with the same class and data than the original
(`osmapi_objects` or `osmapi_changesets`) but with the specified tags'
format.

## Details

Both formats have advantages. Tags in a list of data.frames is a more
compact representation and there is no risk of clashes of column names
and tag keys. Tags in columns make it easier to select rows by tags as
in a regular data.frame. Column name clashes are resolved and the
original key names restored when transformed to tags list format.

By default, functions returning `osmapi_objects` or `osmapi_changesets`
objects, use the the tags in a list column, but can return the results
in a wide format using the parameter `tags_in_columns = TRUE`.

## See also

Other methods:
[`st_as_sf`](https://docs.ropensci.org/osmapiR/reference/st_as_sf.md)

## Examples

``` r
peaks_wide <- osm_get_objects(
  osm_type = "node", osm_id = c(35308286, 1935675367), tags_in_columns = TRUE
)
peaks_list <- tags_wide2list(peaks_wide)

# tags in list format
peaks_list$tags
#> [[1]]
#>               key          value
#> 1             ele        2784.66
#> 2            name Pic du Canigou
#> 3         name:ca Pic del Canigó
#> 4         natural           peak
#> 5      prominence            550
#> 6    summit:cross            yes
#> 7 summit:register             no
#> 
#> [[2]]
#>       key             value
#> 1     ele              1105
#> 2    name Alt de Benicadell
#> 3 natural              peak
#> 

# Select peaks with `prominence` tag
peaks_wide[!is.na(peaks_wide$prominence), ]
#>   osm_type   osm_id visible version changeset           timestamp     user
#> 1     node 35308286    TRUE      17 140341361 2023-08-24 20:19:22 jmaspons
#>        uid        lat       lon members     ele           name        name:ca
#> 1 11725140 42.5189047 2.4565596    NULL 2784.66 Pic du Canigou Pic del Canigó
#>   natural prominence summit:cross summit:register
#> 1    peak        550          yes              no
peaks_list[sapply(peaks_list$tags, function(x) any(x$key == "prominence")), ]
#>   type       id visible version changeset           timestamp     user      uid
#> 1 node 35308286    TRUE      17 140341361 2023-08-24 20:19:22 jmaspons 11725140
#>          lat       lon members
#> 1 42.5189047 2.4565596    NULL
#>                                                                                  tags
#> 1 7 tags: ele=2784.66 | name=Pic du Canigou | name:ca=Pic del Canigó | natural=pea...

cities_list <- osm_get_objects(osm_type = "relation", osm_id = c("40581", "341530"))
# Column name clash:
cities_wide <- tags_list2wide(cities_list)
```
