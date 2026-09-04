# Retrieve notes by bounding box

Returns the existing notes in the specified bounding box. The notes will
be ordered by the date of their last change, the most recent one will be
first.

## Usage

``` r
osm_read_bbox_notes(
  bbox,
  limit = 100,
  closed = 7,
  format = c("R", "sf", "xml", "rss", "json", "gpx")
)
```

## Arguments

- bbox:

  Coordinates for the area to retrieve the notes from
  (`left,bottom,right,top`). Floating point numbers in degrees,
  expressing a valid bounding box, not larger than the configured size
  limit, 25 square degrees, not overlapping the dateline. It can be
  specified by a character, matrix, vector, `bbox` object from sf, a
  `SpatExtent` from terra. Unnamed vectors and matrices will be sorted
  appropriately and must merely be in the order (`x`, `y`, `x`, `y`) or
  `x` in the first column and `y` in the second column.

- limit:

  Specifies the number of entries returned at max. A value between 1 and
  10000 is valid. Default to 100.

- closed:

  Specifies the number of days a note needs to be closed to no longer be
  returned. A value of 0 means only open notes are returned. A value of
  -1 means all notes are returned. Default to 7.

- format:

  Format of the output. Can be `"R"` (default), `"sf"` `"xml"`, `"rss"`,
  `"json"` or `"gpx"`.

## Value

If `format = "R"`, returns a data frame with one map note per row. If
`format = "sf"`, returns a `sf` object from sf.

### `format = "xml"`

Returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) with
the following format:

    <?xml version="1.0" encoding="UTF-8"?>
    <osm version="0.6" generator="OpenStreetMap server" copyright="OpenStreetMap and contributors" attribution="https://www.openstreetmap.org/copyright" license="https://opendatacommons.org/licenses/odbl/1-0/">
      <note lon="0.1000000" lat="51.0000000">
        <id>16659</id>
        <url>https://master.apis.dev.openstreetmap.org/api/0.6/notes/16659</url>
        <comment_url>https://master.apis.dev.openstreetmap.org/api/0.6/notes/16659/comment</comment_url>
        <close_url>https://master.apis.dev.openstreetmap.org/api/0.6/notes/16659/close</close_url>
        <date_created>2019-06-15 08:26:04 UTC</date_created>
        <status>open</status>
        <comments>
          <comment>
            <date>2019-06-15 08:26:04 UTC</date>
            <uid>1234</uid>
            <user>userName</user>
            <user_url>https://master.apis.dev.openstreetmap.org/user/userName</user_url>
            <action>opened</action>
            <text>ThisIsANote</text>
            <html>&lt;p&gt;ThisIsANote&lt;/p&gt;</html>
          </comment>
          ...
        </comments>
      </note>
      ...
    </osm>

### `format = "json"`

Returns a list with the following json structure:

    {
      "type": "FeatureCollection",
      "features": [
        {
          "type": "Feature",
          "geometry": {"type": "Point", "coordinates": [0.1000000, 51.0000000]},
          "properties": {
            "id": 16659,
            "url": "https://master.apis.dev.openstreetmap.org/api/0.6/notes/16659.json",
            "comment_url": "https://master.apis.dev.openstreetmap.org/api/0.6/notes/16659/comment.json",
            "close_url": "https://master.apis.dev.openstreetmap.org/api/0.6/notes/16659/close.json",
            "date_created": "2019-06-15 08:26:04 UTC",
            "status": "open",
            "comments": [
              {"date": "2019-06-15 08:26:04 UTC", "uid": 1234, "user": "userName", "user_url": "https://master.apis.dev.openstreetmap.org/user/userName", "action": "opened", "text": "ThisIsANote", "html": "<p>ThisIsANote</p>"},
              ...
            ]
          }
        }
      ]
    }

### `format = "rss"` & `format = "gpx"`

For `format` in `"rss"`, and `"gpx"`, a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) with
the corresponding format.

## Note

The comment properties (`uid`, `user`, `user_url`) will be omitted if
the comment was anonymous.

## See also

Other get notes' functions:
[`osm_feed_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_feed_notes.md),
[`osm_get_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_get_notes.md),
[`osm_search_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_search_notes.md)

## Examples

``` r
notes <- osm_read_bbox_notes(bbox = c(3.7854767, 39.7837403, 4.3347931, 40.1011851), limit = 10)
## bbox as a character value also works (bbox = "3.7854767,39.7837403,4.3347931,40.1011851").
notes
#>          lon        lat      id
#> 1  3.8399004 40.0015450 5485914
#> 2  3.8414711 39.9770223 5344464
#> 3  4.3015083 39.8332149 5392698
#> 4  3.8390554 39.9246649 5361526
#> 5  4.0681390 39.9053450 5352866
#> 6  4.2644656 39.8906415 5344999
#> 7  4.2639157 39.8907663 5344998
#> 8  3.8308972 39.9973194 5344994
#> 9  3.8699287 39.9423404 5344976
#> 10 4.0436688 40.0337141 5344972
#>                                                        url
#> 1  https://api.openstreetmap.org/api/0.6/notes/5485914.xml
#> 2  https://api.openstreetmap.org/api/0.6/notes/5344464.xml
#> 3  https://api.openstreetmap.org/api/0.6/notes/5392698.xml
#> 4  https://api.openstreetmap.org/api/0.6/notes/5361526.xml
#> 5  https://api.openstreetmap.org/api/0.6/notes/5352866.xml
#> 6  https://api.openstreetmap.org/api/0.6/notes/5344999.xml
#> 7  https://api.openstreetmap.org/api/0.6/notes/5344998.xml
#> 8  https://api.openstreetmap.org/api/0.6/notes/5344994.xml
#> 9  https://api.openstreetmap.org/api/0.6/notes/5344976.xml
#> 10 https://api.openstreetmap.org/api/0.6/notes/5344972.xml
#>                                                        comment_url
#> 1                                                             <NA>
#> 2                                                             <NA>
#> 3  https://api.openstreetmap.org/api/0.6/notes/5392698/comment.xml
#> 4  https://api.openstreetmap.org/api/0.6/notes/5361526/comment.xml
#> 5  https://api.openstreetmap.org/api/0.6/notes/5352866/comment.xml
#> 6  https://api.openstreetmap.org/api/0.6/notes/5344999/comment.xml
#> 7  https://api.openstreetmap.org/api/0.6/notes/5344998/comment.xml
#> 8  https://api.openstreetmap.org/api/0.6/notes/5344994/comment.xml
#> 9  https://api.openstreetmap.org/api/0.6/notes/5344976/comment.xml
#> 10 https://api.openstreetmap.org/api/0.6/notes/5344972/comment.xml
#>                                                        close_url
#> 1                                                           <NA>
#> 2                                                           <NA>
#> 3  https://api.openstreetmap.org/api/0.6/notes/5392698/close.xml
#> 4  https://api.openstreetmap.org/api/0.6/notes/5361526/close.xml
#> 5  https://api.openstreetmap.org/api/0.6/notes/5352866/close.xml
#> 6  https://api.openstreetmap.org/api/0.6/notes/5344999/close.xml
#> 7  https://api.openstreetmap.org/api/0.6/notes/5344998/close.xml
#> 8  https://api.openstreetmap.org/api/0.6/notes/5344994/close.xml
#> 9  https://api.openstreetmap.org/api/0.6/notes/5344976/close.xml
#> 10 https://api.openstreetmap.org/api/0.6/notes/5344972/close.xml
#>           date_created status
#> 1  2026-08-29 19:55:46 closed
#> 2  2026-06-14 12:18:41 closed
#> 3  2026-07-13 04:18:23   open
#> 4  2026-06-25 21:24:13   open
#> 5  2026-06-20 11:13:17   open
#> 6  2026-06-14 17:20:51   open
#> 7  2026-06-14 17:19:04   open
#> 8  2026-06-14 17:18:01   open
#> 9  2026-06-14 17:07:10   open
#> 10 2026-06-14 17:04:36   open
#>                                                           comments
#> 1  2 comments from 2026-08-29 to 2026-09-02 by Ancrou, hectodiu...
#> 2            2 comments from 2026-06-14 to 2026-09-02 by hectodium
#> 3                             1 comment from 2026-07-13 by sasuse2
#> 4                            1 comment from 2026-06-25 by donux-nl
#> 5                               1 comment from 2026-06-20 by neich
#> 6                      1 comment from 2026-06-14 by anonymous user
#> 7                      1 comment from 2026-06-14 by anonymous user
#> 8                      1 comment from 2026-06-14 by anonymous user
#> 9                      1 comment from 2026-06-14 by anonymous user
#> 10                     1 comment from 2026-06-14 by anonymous user
```
