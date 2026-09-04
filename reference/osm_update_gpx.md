# Update GPS trace

Use this to update a GPX info. Only usable by the owner account.
Requires authentication.

## Usage

``` r
osm_update_gpx(
  gpx_id,
  name,
  description,
  tags,
  visibility = c("private", "public", "trackable", "identifiable")
)
```

## Arguments

- gpx_id:

  The id of the track to update represented by a numeric or a character
  value.

- name:

  The file name of the track. Usually, the file name when using
  [`osm_create_gpx()`](https://docs.ropensci.org/osmapiR/reference/osm_create_gpx.md).

- description:

  The trace description.

- tags:

  A string containing tags for the trace that will replace the current
  ones.

- visibility:

  One of the following: `private`, `public`, `trackable`,
  `identifiable`. For explanations see [OSM trace upload
  page](https://www.openstreetmap.org/traces/mine) or [Visibility of GPS
  traces](https://wiki.openstreetmap.org/wiki/Visibility_of_GPS_traces)).

## Value

Returns a data frame with the updated metadata of the GPS trace. The
same format that
[`osm_get_gpx_metadata()`](https://docs.ropensci.org/osmapiR/reference/osm_get_gpx_metadata.md)
with `format = "R"`.

## Details

Missing arguments won't be updated.

## See also

Other edit GPS traces' functions:
[`osm_create_gpx()`](https://docs.ropensci.org/osmapiR/reference/osm_create_gpx.md),
[`osm_delete_gpx()`](https://docs.ropensci.org/osmapiR/reference/osm_delete_gpx.md)

## Examples

``` r
vignette("how_to_edit_gps_traces", package = "osmapiR")
#> Warning: vignette ‘how_to_edit_gps_traces’ not found
```
