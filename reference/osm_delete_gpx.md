# Delete GPS traces

Use this to delete GPX files. Only usable by the owner account. Requires
authentication.

## Usage

``` r
osm_delete_gpx(gpx_id)
```

## Arguments

- gpx_id:

  The track ids represented by a numeric or a character vector.

## Value

Returns `NULL` invisibly.

## See also

Other edit GPS traces' functions:
[`osm_create_gpx()`](https://docs.ropensci.org/osmapiR/reference/osm_create_gpx.md),
[`osm_update_gpx()`](https://docs.ropensci.org/osmapiR/reference/osm_update_gpx.md)

## Examples

``` r
vignette("how_to_edit_gps_traces", package = "osmapiR")
#> Warning: vignette ‘how_to_edit_gps_traces’ not found
```
