# Create GPS trace

Use this to upload a GPX file or archive of GPX files. Requires
authentication.

## Usage

``` r
osm_create_gpx(
  file,
  description,
  tags,
  visibility = c("trackable", "identifiable")
)
```

## Arguments

- file:

  The GPX file path containing the track points.

- description:

  The trace description. Cannot be empty. Maximum length is 255
  characters.

- tags:

  A string containing tags for the trace. Can be empty.

- visibility:

  One of the following: `trackable`, `identifiable`. For explanations
  see [OSM trace upload page](https://www.openstreetmap.org/traces/mine)
  or [Visibility of GPS
  traces](https://wiki.openstreetmap.org/wiki/Visibility_of_GPS_traces)).

## Value

A number representing the ID of the new gpx.

## Details

Note that for successful processing, the file must contain trackpoints
(`<trkpt>`), not only waypoints, and the trackpoints must have a valid
timestamp. Since the file is processed asynchronously, the call will
complete successfully even if the file cannot be processed. The file may
also be a .tar, .tar.gz or .zip containing multiple gpx files, although
it will appear as a single entry in the upload log.

## See also

Other edit GPS traces' functions:
[`osm_delete_gpx()`](https://docs.ropensci.org/osmapiR/reference/osm_delete_gpx.md),
[`osm_update_gpx()`](https://docs.ropensci.org/osmapiR/reference/osm_update_gpx.md)

## Examples

``` r
vignette("how_to_edit_gps_traces", package = "osmapiR")
#> Warning: vignette ‘how_to_edit_gps_traces’ not found
```
