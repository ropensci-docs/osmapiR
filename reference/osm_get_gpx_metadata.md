# Download GPS Track Metadata

Use this to access the metadata about GPX files. Available without
authentication if the file is marked public. Otherwise only usable by
the owner account and requires authentication.

## Usage

``` r
osm_get_gpx_metadata(gpx_id, format = c("R", "sf", "xml", "json"))
```

## Arguments

- gpx_id:

  A vector of track ids represented by a numeric or a character value.

- format:

  Format of the output. Can be `"R"` (default), `"sf"`, `"xml"`, or
  `"json"`.

## Value

If `format = "R"`, returns a data frame with one trace per row. If
`format = "sf"`, returns a `sf` object from sf. If `format = "xml"`,
returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) with
the following format:

    <?xml version="1.0" encoding="UTF-8"?>
    <osm version="0.6" generator="OpenStreetMap server">
      <gpx_file id="836619" name="track.gpx" lat="52.0194" lon="8.51807" uid="1234" user="Hartmut Holzgraefe" visibility="public" pending="false" timestamp="2010-10-09T09:24:19Z">
        <description>PHP upload test</description>
        <tag>test</tag>
        <tag>php</tag>
      </gpx_file>
      <gpx_file>
        ...
      </gpx_file>
    </osm>

If `format = "json"`, returns a list with the json structure.

## See also

Other get GPS' functions:
[`osm_get_data_gpx()`](https://docs.ropensci.org/osmapiR/reference/osm_get_data_gpx.md),
[`osm_get_points_gps()`](https://docs.ropensci.org/osmapiR/reference/osm_get_points_gps.md),
[`osm_list_gpxs()`](https://docs.ropensci.org/osmapiR/reference/osm_list_gpxs.md)

## Examples

``` r
if (FALSE) { # \dontrun{
trk_meta <- osm_get_gpx_metadata(gpx_id = 3498170)
trk_meta
} # }
```
