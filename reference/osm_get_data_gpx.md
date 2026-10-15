# Download GPS Track Data

Use this to download the full GPX file. Private and trackable traces are
only available by the owner account. Requires authentication.

## Usage

``` r
osm_get_data_gpx(gpx_id, format)
```

## Arguments

- gpx_id:

  The track id represented by a numeric or a character value.

- format:

  Format of the output. If missing (default), the response will be the
  exact file that was uploaded. If `"R"`, a `data.frame`. If
  `"sf_lines"` (`"sf"` is a synonym for `"sf_lines"`) or `"sf_points"`,
  a `sf` object from package sf. If `"gpx"`, the response will always be
  a GPX format file. If `"xml"`, a `xml` file in an undocumented format.

## Value

If missing `format`, returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) with
the original file data. If `format = "R"`, returns a data frame with one
point per row and the attributes extracted from the xml response. If
`format = "sf*"`, returns a `sf` object from sf (see
[`st_as_sf()`](https://docs.ropensci.org/osmapiR/reference/st_as_sf.md)
for details). If `format = "gpx"`, returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) in the
GPX format. If `format = "xml"`, returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) in an
undocumented format.

## Note

If you request refers to a multi-file archive the response when you
force `gpx` or `xml` format will consist of a non-standard simple
concatenation of the files.

Extended data following schema
[`http://www.garmin.com/xmlschemas/TrackPointExtension/v1`](https://www8.garmin.com/xmlschemas/GpxExtensions/v3/GpxExtensionsv3.xsd)
in gpx files will be extracted for `format = "R"` and
`format = "sf_points"`, but lost for `format = "sf_line"`.

## See also

Other get GPS' functions:
[`osm_get_gpx_metadata()`](https://docs.ropensci.org/osmapiR/reference/osm_get_gpx_metadata.md),
[`osm_get_points_gps()`](https://docs.ropensci.org/osmapiR/reference/osm_get_points_gps.md),
[`osm_list_gpxs()`](https://docs.ropensci.org/osmapiR/reference/osm_list_gpxs.md)

## Examples

``` r
if (FALSE) { # \dontrun{
trk_data <- osm_get_data_gpx(gpx_id = 3498170, format = "R")
trk_data

## get attributes
attr(trk_data, "track")
attr(trk_data, "gpx_attributes")
} # }
```
