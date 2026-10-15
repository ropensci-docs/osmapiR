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
#> 1  4.2648239 39.8903577 5561227
#> 2  4.2639157 39.8907663 5344998
#> 3  4.2334754 39.8899198 4389224
#> 4  4.2383816 39.8863113 5545093
#> 5  3.9653895 39.9389582 5271470
#> 6  4.2773460 39.8811322 5518350
#> 7  4.2659586 39.8887002 5509668
#> 8  4.2659586 39.8887002 5509662
#> 9  4.3015083 39.8332149 5392698
#> 10 3.8390554 39.9246649 5361526
#>                                                        url
#> 1  https://api.openstreetmap.org/api/0.6/notes/5561227.xml
#> 2  https://api.openstreetmap.org/api/0.6/notes/5344998.xml
#> 3  https://api.openstreetmap.org/api/0.6/notes/4389224.xml
#> 4  https://api.openstreetmap.org/api/0.6/notes/5545093.xml
#> 5  https://api.openstreetmap.org/api/0.6/notes/5271470.xml
#> 6  https://api.openstreetmap.org/api/0.6/notes/5518350.xml
#> 7  https://api.openstreetmap.org/api/0.6/notes/5509668.xml
#> 8  https://api.openstreetmap.org/api/0.6/notes/5509662.xml
#> 9  https://api.openstreetmap.org/api/0.6/notes/5392698.xml
#> 10 https://api.openstreetmap.org/api/0.6/notes/5361526.xml
#>                                                        comment_url
#> 1  https://api.openstreetmap.org/api/0.6/notes/5561227/comment.xml
#> 2  https://api.openstreetmap.org/api/0.6/notes/5344998/comment.xml
#> 3  https://api.openstreetmap.org/api/0.6/notes/4389224/comment.xml
#> 4  https://api.openstreetmap.org/api/0.6/notes/5545093/comment.xml
#> 5  https://api.openstreetmap.org/api/0.6/notes/5271470/comment.xml
#> 6  https://api.openstreetmap.org/api/0.6/notes/5518350/comment.xml
#> 7  https://api.openstreetmap.org/api/0.6/notes/5509668/comment.xml
#> 8  https://api.openstreetmap.org/api/0.6/notes/5509662/comment.xml
#> 9  https://api.openstreetmap.org/api/0.6/notes/5392698/comment.xml
#> 10 https://api.openstreetmap.org/api/0.6/notes/5361526/comment.xml
#>                                                        close_url
#> 1  https://api.openstreetmap.org/api/0.6/notes/5561227/close.xml
#> 2  https://api.openstreetmap.org/api/0.6/notes/5344998/close.xml
#> 3  https://api.openstreetmap.org/api/0.6/notes/4389224/close.xml
#> 4  https://api.openstreetmap.org/api/0.6/notes/5545093/close.xml
#> 5  https://api.openstreetmap.org/api/0.6/notes/5271470/close.xml
#> 6  https://api.openstreetmap.org/api/0.6/notes/5518350/close.xml
#> 7  https://api.openstreetmap.org/api/0.6/notes/5509668/close.xml
#> 8  https://api.openstreetmap.org/api/0.6/notes/5509662/close.xml
#> 9  https://api.openstreetmap.org/api/0.6/notes/5392698/close.xml
#> 10 https://api.openstreetmap.org/api/0.6/notes/5361526/close.xml
#>           date_created status
#> 1  2026-10-08 09:28:18   open
#> 2  2026-06-14 17:19:04   open
#> 3  2024-08-18 07:34:42   open
#> 4  2026-09-29 08:50:27   open
#> 5  2026-04-29 16:35:41   open
#> 6  2026-09-14 07:12:03   open
#> 7  2026-09-09 15:58:26   open
#> 8  2026-09-09 15:53:07   open
#> 9  2026-07-13 04:18:23   open
#> 10 2026-06-25 21:24:13   open
#>                                                           comments
#> 1                            1 comment from 2026-10-08 by TrixTrax
#> 2         2 comments from 2026-06-14 to 2026-10-08 by NA, TrixTrax
#> 3       3 comments from 2024-08-18 to 2026-09-29 by dnix, TrixTrax
#> 4                            1 comment from 2026-09-29 by TrixTrax
#> 5  3 comments from 2026-04-29 to 2026-09-26 by donux-nl, TrixTr...
#> 6                      1 comment from 2026-09-14 by anonymous user
#> 7                            1 comment from 2026-09-09 by Steph731
#> 8                            1 comment from 2026-09-09 by Steph731
#> 9                             1 comment from 2026-07-13 by sasuse2
#> 10                           1 comment from 2026-06-25 by donux-nl
```
