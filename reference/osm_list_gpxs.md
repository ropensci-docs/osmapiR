# List user's GPX traces

Use this to get a list of GPX traces owned by the authenticated user.
Requires authentication.

## Usage

``` r
osm_list_gpxs(format = c("R", "sf", "xml"))
```

## Arguments

- format:

  Format of the output. Can be `"R"` (default), `"sf"` or `"xml"`.

## Value

Results with the same format as
[`osm_get_gpx_metadata()`](https://docs.ropensci.org/osmapiR/reference/osm_get_gpx_metadata.md).
If `format = "R"`, returns a data frame with one trace per row. If
`format = "sf"`, returns a `sf` object from sf. If `format = "xml"`,
returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md).
Example:

    <?xml version="1.0" encoding="UTF-8"?>
    <osm version="0.6" generator="OpenStreetMap server">
      <gpx_file id="836619" name="track.gpx" lat="52.0194" lon="8.51807" uid="1234" user="Hartmut Holzgraefe" visibility="public" pending="false" timestamp="2010-10-09T09:24:19Z">
        <description>PHP upload test</description>
        <tag>test</tag>
        <tag>php</tag>
      </gpx_file>
      <gpx_file id="836620" name="track.gpx" lat="52.1194" lon="8.61807" uid="1234" user="Hartmut Holzgraefe" visibility="public" pending="false" timestamp="2010-10-09T09:27:31Z">
        <description>PHP upload test 2</description>
        <tag>test</tag>
        <tag>php</tag>
      </gpx_file>
    </osm>

## See also

Other get GPS' functions:
[`osm_get_data_gpx()`](https://docs.ropensci.org/osmapiR/reference/osm_get_data_gpx.md),
[`osm_get_gpx_metadata()`](https://docs.ropensci.org/osmapiR/reference/osm_get_gpx_metadata.md),
[`osm_get_points_gps()`](https://docs.ropensci.org/osmapiR/reference/osm_get_points_gps.md)

## Examples

``` r
if (FALSE) { # \dontrun{
traces <- osm_list_gpxs()
traces
} # }
```
