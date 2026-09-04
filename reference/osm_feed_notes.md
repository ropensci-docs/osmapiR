# RSS Feed of notes in a bbox

RSS Feed of notes in a bbox

## Usage

``` r
osm_feed_notes(bbox)
```

## Arguments

- bbox:

  Coordinates for the area to retrieve the notes from
  (`left,bottom,right,top`). Floating point numbers in degrees,
  expressing a valid bounding box, not larger than the configured size
  limit, 25 square degrees (see `osm_capabilities()$note_area` and [this
  line in
  settings](https://github.com/openstreetmap/openstreetmap-website/blob/master/config/settings.yml#L27)
  for the current value), not overlapping the dateline. It can be
  specified by a character, matrix, vector, `bbox` object from sf, a
  `SpatExtent` from terra. Unnamed vectors and matrices will be sorted
  appropriately and must merely be in the order (`x`, `y`, `x`, `y`) or
  `x` in the first column and `y` in the second column.

## Value

Returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) in the
`RSS` format.

## See also

Other get notes' functions:
[`osm_get_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_get_notes.md),
[`osm_read_bbox_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_read_bbox_notes.md),
[`osm_search_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_search_notes.md)

## Examples

``` r
feed_notes <- osm_feed_notes(bbox = c(0.8205414, 40.6686604, 0.8857727, 40.7493377))
## bbox as a character value also works (bbox = "0.8205414,40.6686604,0.8857727,40.7493377").
feed_notes
#> {xml_document}
#> <rss version="2.0" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:geo="http://www.w3.org/2003/01/geo/wgs84_pos#" xmlns:georss="http://www.georss.org/georss">
#> [1] <channel>\n  <title>OpenStreetMap Notes</title>\n  <description>A list of ...
```
