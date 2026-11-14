# Convert osmapiR objects to sf objects

Convert osmapiR objects to sf objects

## Usage

``` r
st_as_sf.osmapi_map_notes(x, ...)

st_as_sf.osmapi_changesets(x, ...)

st_as_sf.osmapi_gps_track(x, format = c("line", "points"), ...)

st_as_sf.osmapi_gpx(x, format = c("lines", "points"), ...)
```

## Arguments

- x:

  an osmapiR object.

- ...:

  passed on to `st_as_sf()` from sf package.

- format:

  Format of the output. If `"line"` (the default), return a `sf` object
  with one `LINESTRING` for each track. If `"points"`, return a `sf`
  with the `POINT`s of the track as features. See below for details.

## Value

Returns a `sf` object from sf package or a list of for `osmapi_gpx` and
`format = "points"`.

When x is a `osmapi_gps_track` or `osmapi_gpx` object and
`format = "line"`, the result will have `XYZM` dimensions for
coordinates, elevation and time if available. In this format, time will
loss the POSIXct type as only numeric values are allowed. For
`format = "points"`, the result will have `XY` dimensions and elevation
and time will be independent columns if available.

## See also

`st_as_sf()` from sf package.

Other methods:
[`tags_list2wide()`](https://docs.ropensci.org/osmapiR/reference/tags_list-wide.md)

## Examples

``` r
note <- osm_get_notes(note_id = "2067786")
sf::st_as_sf(note)
#> Simple feature collection with 1 feature and 7 fields
#> Geometry type: POINT
#> Dimension:     XY
#> Bounding box:  xmin: 1.72146 ymin: 42.03322 xmax: 1.72146 ymax: 42.03322
#> Geodetic CRS:  WGS 84
#>        id                                                     url comment_url
#> 1 2067786 https://api.openstreetmap.org/api/0.6/notes/2067786.xml        <NA>
#>   close_url        date_created status
#> 1      <NA> 2020-01-24 18:21:48 closed
#>                                                          comments
#> 1 3 comments from 2020-01-24 to 2024-06-12 by Juliosebastian, ...
#>                   geometry
#> 1 POINT (1.72146 42.03322)

chaset <- osm_get_changesets(changeset_id = 137595351, include_discussion = TRUE)
sf::st_as_sf(chaset)
#> Simple feature collection with 1 feature and 10 fields
#> Geometry type: POLYGON
#> Dimension:     XY
#> Bounding box:  xmin: 2.658056 ymin: 42.67996 xmax: 2.712578 ymax: 42.69368
#> Geodetic CRS:  WGS 84
#>          id          created_at           closed_at  open      user      uid
#> 1 137595351 2023-06-21 09:09:18 2023-06-21 09:09:18 FALSE Quercinus 19641470
#>   comments_count changes_count
#> 1              4             1
#>                                                     discussion
#> 1 4 comments from 2023-06-26 to 2023-07-03 by rainerU, Quer...
#>                                                                                  tags
#> 1 8 tags: changesets_count=1 | comment=Correcció d'acord amb la toponímia oficial ...
#>                         geometry
#> 1 POLYGON ((2.658056 42.67996...

gpx <- osm_get_points_gps(bbox = c(-0.3667545, 40.2153246, -0.3354263, 40.2364915))
sf::st_as_sf(gpx, format = "line")
#> Simple feature collection with 4 features and 3 fields
#> Geometry type: LINESTRING
#> Dimension:     XYM
#> Bounding box:  xmin: -0.3667491 ymin: 40.21533 xmax: -0.335427 ymax: 40.23649
#> m_range:       mmin: 1725702000 mmax: 1725731000
#> Geodetic CRS:  WGS 84
#>   track_url track_name track_desc                       geometry
#> 1      <NA>       <NA>       <NA> LINESTRING M (-0.3540273 40...
#> 2      <NA>       <NA>       <NA> LINESTRING M (-0.3540273 40...
#> 3      <NA>       <NA>       <NA> LINESTRING M (-0.3667491 40...
#> 4      <NA>       <NA>       <NA> LINESTRING M (-0.335428 40....
sf::st_as_sf(gpx, format = "points")
#> [[1]]
#> Simple feature collection with 1228 features and 1 field
#> Geometry type: POINT
#> Dimension:     XY
#> Bounding box:  xmin: -0.3666823 ymin: 40.21658 xmax: -0.335464 ymax: 40.23649
#> Geodetic CRS:  WGS 84
#> First 10 features:
#>                   time                    geometry
#> 1  2024-09-07 09:41:03 POINT (-0.3540273 40.23649)
#> 2  2024-09-07 09:41:09 POINT (-0.3540151 40.23643)
#> 3  2024-09-07 09:41:15 POINT (-0.3540038 40.23637)
#> 4  2024-09-07 09:41:21 POINT (-0.3539977 40.23631)
#> 5  2024-09-07 09:41:27 POINT (-0.3540082 40.23625)
#> 6  2024-09-07 09:41:33 POINT (-0.3539839 40.23619)
#> 7  2024-09-07 09:41:39 POINT (-0.3539756 40.23612)
#> 8  2024-09-07 09:41:45  POINT (-0.353958 40.23606)
#> 9  2024-09-07 09:41:51 POINT (-0.3539329 40.23601)
#> 10 2024-09-07 09:41:57 POINT (-0.3539372 40.23596)
#> 
#> $`/user/Jordi%20MF/traces/11454866`
#> Simple feature collection with 1351 features and 1 field
#> Geometry type: POINT
#> Dimension:     XY
#> Bounding box:  xmin: -0.3666823 ymin: 40.21533 xmax: -0.335464 ymax: 40.23649
#> Geodetic CRS:  WGS 84
#> First 10 features:
#>                   time                    geometry
#> 1  2024-09-07 09:41:03 POINT (-0.3540273 40.23649)
#> 2  2024-09-07 09:41:09 POINT (-0.3540151 40.23643)
#> 3  2024-09-07 09:41:15 POINT (-0.3540038 40.23637)
#> 4  2024-09-07 09:41:21 POINT (-0.3539977 40.23631)
#> 5  2024-09-07 09:41:27 POINT (-0.3540082 40.23625)
#> 6  2024-09-07 09:41:33 POINT (-0.3539839 40.23619)
#> 7  2024-09-07 09:41:39 POINT (-0.3539756 40.23612)
#> 8  2024-09-07 09:41:45  POINT (-0.353958 40.23606)
#> 9  2024-09-07 09:41:51 POINT (-0.3539329 40.23601)
#> 10 2024-09-07 09:41:57 POINT (-0.3539372 40.23596)
#> 
#> $`/user/Jordi%20MF/traces/11408449`
#> Simple feature collection with 770 features and 1 field
#> Geometry type: POINT
#> Dimension:     XY
#> Bounding box:  xmin: -0.3667491 ymin: 40.22847 xmax: -0.3487916 ymax: 40.23649
#> Geodetic CRS:  WGS 84
#> First 10 features:
#>                   time                    geometry
#> 1  2024-07-23 14:18:49 POINT (-0.3667491 40.23328)
#> 2  2024-07-23 14:18:53 POINT (-0.3667264 40.23323)
#> 3  2024-07-23 14:18:57 POINT (-0.3667052 40.23318)
#> 4  2024-07-23 14:19:01 POINT (-0.3666983 40.23314)
#> 5  2024-07-23 14:19:07 POINT (-0.3666966 40.23307)
#> 6  2024-07-23 14:19:11 POINT (-0.3666911 40.23302)
#> 7  2024-07-23 14:19:17 POINT (-0.3666864 40.23296)
#> 8  2024-07-23 14:19:23  POINT (-0.3666881 40.2329)
#> 9  2024-07-23 14:19:29 POINT (-0.3666841 40.23283)
#> 10 2024-07-23 14:19:35 POINT (-0.3666788 40.23278)
#> 
#> $`/user/IslaDeva/traces/11288482`
#> Simple feature collection with 1651 features and 1 field
#> Geometry type: POINT
#> Dimension:     XY
#> Bounding box:  xmin: -0.349267 ymin: 40.2187 xmax: -0.335427 ymax: 40.23148
#> Geodetic CRS:  WGS 84
#> First 10 features:
#>                   time                   geometry
#> 1  2024-02-17 08:29:04  POINT (-0.335428 40.2187)
#> 2  2024-02-17 08:29:05 POINT (-0.335432 40.21871)
#> 3  2024-02-17 08:29:06 POINT (-0.335432 40.21872)
#> 4  2024-02-17 08:29:07 POINT (-0.335432 40.21872)
#> 5  2024-02-17 08:32:37 POINT (-0.335427 40.22013)
#> 6  2024-02-17 08:32:38 POINT (-0.335427 40.22013)
#> 7  2024-02-17 08:32:39 POINT (-0.335452 40.22015)
#> 8  2024-02-17 08:32:40  POINT (-0.33546 40.22016)
#> 9  2024-02-17 08:32:41 POINT (-0.335475 40.22017)
#> 10 2024-02-17 08:32:42 POINT (-0.335487 40.22018)
#> 
#> attr(,"class")
#> [1] "sf_osmapi_gpx" "osmapi_gpx"    "list"         
#> attr(,"gpx_attributes")
#>                             version                             creator 
#>                               "1.0"                 "OpenStreetMap.org" 
#>                               xmlns 
#> "http://www.topografix.com/GPX/1/0" 

if (FALSE) { # \dontrun{
# Requires authentication
trk <- osm_get_data_gpx(gpx_id = 3498170, format = "R")
sf::st_as_sf(trk, format = "line")
sf::st_as_sf(trk, format = "points")
} # }
```
