# Get notes

Returns the existing note with the given ID.

## Usage

``` r
osm_get_notes(note_id, format = c("R", "sf", "xml", "rss", "json", "gpx"))
```

## Arguments

- note_id:

  Note id represented by a numeric or a character value.

- format:

  Format of the output. Can be `"R"` (default), `"sf"`, `"xml"`,
  `"rss"`, `"json"` or `"gpx"`.

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

## See also

Other get notes' functions:
[`osm_feed_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_feed_notes.md),
[`osm_read_bbox_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_read_bbox_notes.md),
[`osm_search_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_search_notes.md)

## Examples

``` r
note <- osm_get_notes(note_id = "2067786")
note
#>         lon        lat      id
#> 1 1.7214600 42.0332200 2067786
#>                                                       url comment_url close_url
#> 1 https://api.openstreetmap.org/api/0.6/notes/2067786.xml        <NA>      <NA>
#>          date_created status
#> 1 2020-01-24 18:21:48 closed
#>                                                          comments
#> 1 3 comments from 2020-01-24 to 2024-06-12 by Juliosebastian, ...
```
