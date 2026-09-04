# Search for notes

Returns notes that match the specified query. If no query is provided,
the most recently updated notes are returned.

## Usage

``` r
osm_search_notes(
  q,
  user,
  bbox,
  from,
  to,
  closed = 7,
  sort = c("created_at", "updated_at"),
  order = c("newest", "oldest"),
  limit = getOption("osmapir.api_capabilities")$api$notes["default_query_limit"],
  format = c("R", "sf", "xml", "rss", "json", "gpx")
)
```

## Arguments

- q:

  Text search query, matching either note text or comments.

- user:

  Search for notes which the given user interacted with. The value can
  be the user id (`numeric`) or the display name (`character`).

- bbox:

  Search area expressed as a string or a numeric vector of 4 coordinates
  of a valid bounding box (`left,bottom,right,top`) in decimal degrees.
  It can be specified by a character, matrix, vector, `bbox` object from
  sf, a `SpatExtent` from terra. Unnamed vectors and matrices will be
  sorted appropriately and must merely be in the order (`x`, `y`, `x`,
  `y`) or `x` in the first column and `y` in the second column. Area
  must be at most 25 square degrees (see `osm_capabilities()$note_area`
  and [this line in
  settings](https://github.com/openstreetmap/openstreetmap-website/blob/master/config/settings.yml#L27)
  for the current value).

- from:

  Beginning date range for `created_at` or `updated_at` (specified by
  `sort`). Preferably in [ISO
  8601](https://en.wikipedia.org/wiki/ISO_8601) date format.

- to:

  End date range for `created_at` or `updated_at` (specified by `sort`).
  Preferably in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date
  format. Only works when `from` is supplied.

- closed:

  Specifies the number of days a note needs to be closed to no longer be
  returned. A value of 0 means only open notes are returned. A value of
  -1 means all notes are returned. 7 is the default.

- sort:

  Sort results by creation (`"created_at"`, the default) or update date
  (`"updated_at"`).

- order:

  Sorting order. `"oldest"` is ascending order, `"newest"` is descending
  order (the default).

- limit:

  Maximum number of results between 1 and 10000 (may change, see
  `osm_capabilities()$api$notes` for the current value). Default to 100.

- format:

  Format of the the returned list of notes. Can be `"R"` (default),
  `"sf"`, `"xml"`, `"rss"`, `"json"` or `"gpx"`.

## Value

If `format = "R"`, returns a data frame with one map note per row. If
`format = "sf"`, returns a `sf` object from sf. If `format = "json"`,
returns a list with the json structure. For `format` in `"xml"`,
`"rss"`, and `"gpx"`, a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) with
the corresponding format.

## Details

The notes will be ordered by the date of their last change, the most
recent one will be first.

## See also

Other get notes' functions:
[`osm_feed_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_feed_notes.md),
[`osm_get_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_get_notes.md),
[`osm_read_bbox_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_read_bbox_notes.md)

## Examples

``` r
notes <- osm_search_notes(
  q = "POI", bbox = "0.1594133,40.5229822,3.3222508,42.8615226",
  from = "2017-10-01", to = "2018-10-27T15:27A", limit = 10
)
notes
#> [1] lon          lat          id           url          comment_url 
#> [6] close_url    date_created status       comments    
#> <0 rows> (or 0-length row.names)

my_notes <- osm_search_notes(
  user = "jmaspons", bbox = c(-0.1594133, 40.5229822, 3.322251, 42.861523),
  closed = -1, format = "json"
)
my_notes
#> $type
#> [1] "FeatureCollection"
#> 
#> $features
#> $features[[1]]
#> $features[[1]]$type
#> [1] "Feature"
#> 
#> $features[[1]]$geometry
#> $features[[1]]$geometry$type
#> [1] "Point"
#> 
#> $features[[1]]$geometry$coordinates
#> $features[[1]]$geometry$coordinates[[1]]
#> [1] 0.45428
#> 
#> $features[[1]]$geometry$coordinates[[2]]
#> [1] 42.68044
#> 
#> 
#> 
#> $features[[1]]$properties
#> $features[[1]]$properties$id
#> [1] 5475480
#> 
#> $features[[1]]$properties$url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/5475480.json"
#> 
#> $features[[1]]$properties$comment_url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/5475480/comment.json"
#> 
#> $features[[1]]$properties$close_url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/5475480/close.json"
#> 
#> $features[[1]]$properties$date_created
#> [1] "2026-08-24 15:55:29 UTC"
#> 
#> $features[[1]]$properties$status
#> [1] "open"
#> 
#> $features[[1]]$properties$comments
#> $features[[1]]$properties$comments[[1]]
#> $features[[1]]$properties$comments[[1]]$date
#> [1] "2026-08-24 15:55:29 UTC"
#> 
#> $features[[1]]$properties$comments[[1]]$uid
#> [1] 11725140
#> 
#> $features[[1]]$properties$comments[[1]]$user
#> [1] "jmaspons"
#> 
#> $features[[1]]$properties$comments[[1]]$user_url
#> [1] "https://api.openstreetmap.org/user/jmaspons"
#> 
#> $features[[1]]$properties$comments[[1]]$action
#> [1] "opened"
#> 
#> $features[[1]]$properties$comments[[1]]$text
#> [1] "Encara existeix? No la he trobat"
#> 
#> $features[[1]]$properties$comments[[1]]$html
#> [1] "<p dir=\"auto\">Encara existeix? No la he trobat</p>"
#> 
#> 
#> 
#> 
#> 
#> $features[[2]]
#> $features[[2]]$type
#> [1] "Feature"
#> 
#> $features[[2]]$geometry
#> $features[[2]]$geometry$type
#> [1] "Point"
#> 
#> $features[[2]]$geometry$coordinates
#> $features[[2]]$geometry$coordinates[[1]]
#> [1] 2.12512
#> 
#> $features[[2]]$geometry$coordinates[[2]]
#> [1] 41.30411
#> 
#> 
#> 
#> $features[[2]]$properties
#> $features[[2]]$properties$id
#> [1] 5280388
#> 
#> $features[[2]]$properties$url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/5280388.json"
#> 
#> $features[[2]]$properties$comment_url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/5280388/comment.json"
#> 
#> $features[[2]]$properties$close_url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/5280388/close.json"
#> 
#> $features[[2]]$properties$date_created
#> [1] "2026-05-06 05:59:26 UTC"
#> 
#> $features[[2]]$properties$status
#> [1] "open"
#> 
#> $features[[2]]$properties$comments
#> $features[[2]]$properties$comments[[1]]
#> $features[[2]]$properties$comments[[1]]$date
#> [1] "2026-05-06 05:59:26 UTC"
#> 
#> $features[[2]]$properties$comments[[1]]$uid
#> [1] 11725140
#> 
#> $features[[2]]$properties$comments[[1]]$user
#> [1] "jmaspons"
#> 
#> $features[[2]]$properties$comments[[1]]$user_url
#> [1] "https://api.openstreetmap.org/user/jmaspons"
#> 
#> $features[[2]]$properties$comments[[1]]$action
#> [1] "opened"
#> 
#> $features[[2]]$properties$comments[[1]]$text
#> [1] "Pont \n\nvia StreetComplete_ee 63.1\n\nAttached photo(s):\nhttps://streetcomplete.app/p/343002.jpg"
#> 
#> $features[[2]]$properties$comments[[1]]$html
#> [1] "<p dir=\"auto\">Pont </p>\n\n<p dir=\"auto\">via StreetComplete_ee 63.1</p>\n\n<p dir=\"auto\">Attached photo(s):\n<br /><a href=\"https://streetcomplete.app/p/343002.jpg\" rel=\"nofollow noopener noreferrer\" dir=\"auto\">https://streetcomplete.app/p/343002.jpg</a></p>"
#> 
#> 
#> 
#> 
#> 
#> $features[[3]]
#> $features[[3]]$type
#> [1] "Feature"
#> 
#> $features[[3]]$geometry
#> $features[[3]]$geometry$type
#> [1] "Point"
#> 
#> $features[[3]]$geometry$coordinates
#> $features[[3]]$geometry$coordinates[[1]]
#> [1] 2.489406
#> 
#> $features[[3]]$geometry$coordinates[[2]]
#> [1] 42.18185
#> 
#> 
#> 
#> $features[[3]]$properties
#> $features[[3]]$properties$id
#> [1] 4976991
#> 
#> $features[[3]]$properties$url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/4976991.json"
#> 
#> $features[[3]]$properties$comment_url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/4976991/comment.json"
#> 
#> $features[[3]]$properties$close_url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/4976991/close.json"
#> 
#> $features[[3]]$properties$date_created
#> [1] "2025-09-24 05:22:19 UTC"
#> 
#> $features[[3]]$properties$status
#> [1] "open"
#> 
#> $features[[3]]$properties$comments
#> $features[[3]]$properties$comments[[1]]
#> $features[[3]]$properties$comments[[1]]$date
#> [1] "2025-09-24 05:22:19 UTC"
#> 
#> $features[[3]]$properties$comments[[1]]$uid
#> [1] 11725140
#> 
#> $features[[3]]$properties$comments[[1]]$user
#> [1] "jmaspons"
#> 
#> $features[[3]]$properties$comments[[1]]$user_url
#> [1] "https://api.openstreetmap.org/user/jmaspons"
#> 
#> $features[[3]]$properties$comments[[1]]$action
#> [1] "opened"
#> 
#> $features[[3]]$properties$comments[[1]]$text
#> [1] "nom local Plaça de l'Àngel per l'escultura que hi ha. Cal confirmació aborigen\n\n#OsmAnd"
#> 
#> $features[[3]]$properties$comments[[1]]$html
#> [1] "<p dir=\"auto\">nom local Plaça de l'Àngel per l'escultura que hi ha. Cal confirmació aborigen</p>\n\n<p dir=\"auto\">#OsmAnd</p>"
#> 
#> 
#> 
#> 
#> 
#> $features[[4]]
#> $features[[4]]$type
#> [1] "Feature"
#> 
#> $features[[4]]$geometry
#> $features[[4]]$geometry$type
#> [1] "Point"
#> 
#> $features[[4]]$geometry$coordinates
#> $features[[4]]$geometry$coordinates[[1]]
#> [1] 1.390606
#> 
#> $features[[4]]$geometry$coordinates[[2]]
#> [1] 42.6192
#> 
#> 
#> 
#> $features[[4]]$properties
#> $features[[4]]$properties$id
#> [1] 4955393
#> 
#> $features[[4]]$properties$url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/4955393.json"
#> 
#> $features[[4]]$properties$comment_url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/4955393/comment.json"
#> 
#> $features[[4]]$properties$close_url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/4955393/close.json"
#> 
#> $features[[4]]$properties$date_created
#> [1] "2025-09-10 08:00:49 UTC"
#> 
#> $features[[4]]$properties$status
#> [1] "open"
#> 
#> $features[[4]]$properties$comments
#> $features[[4]]$properties$comments[[1]]
#> $features[[4]]$properties$comments[[1]]$date
#> [1] "2025-09-10 08:00:49 UTC"
#> 
#> $features[[4]]$properties$comments[[1]]$uid
#> [1] 11725140
#> 
#> $features[[4]]$properties$comments[[1]]$user
#> [1] "jmaspons"
#> 
#> $features[[4]]$properties$comments[[1]]$user_url
#> [1] "https://api.openstreetmap.org/user/jmaspons"
#> 
#> $features[[4]]$properties$comments[[1]]$action
#> [1] "opened"
#> 
#> $features[[4]]$properties$comments[[1]]$text
#> [1] "Unable to answer \"This shop has been vacant. What’s here now?\" – Cabana de Boet (Building) – https://osm.org/way/430288660 via StreetComplete_ee 61.1:\n\nEl pis de baix és un corral que està obert, s'hi pot dormir en cas d'emergència. El pis de dalt està tancat."
#> 
#> $features[[4]]$properties$comments[[1]]$html
#> [1] "<p dir=\"auto\">Unable to answer \"This shop has been vacant. What’s here now?\" – Cabana de Boet (Building) – <a href=\"https://osm.org/way/430288660\" rel=\"nofollow noopener noreferrer\" dir=\"auto\">way/430288660</a> via StreetComplete_ee 61.1:</p>\n\n<p dir=\"auto\">El pis de baix és un corral que està obert, s'hi pot dormir en cas d'emergència. El pis de dalt està tancat.</p>"
#> 
#> 
#> 
#> 
#> 
#> $features[[5]]
#> $features[[5]]$type
#> [1] "Feature"
#> 
#> $features[[5]]$geometry
#> $features[[5]]$geometry$type
#> [1] "Point"
#> 
#> $features[[5]]$geometry$coordinates
#> $features[[5]]$geometry$coordinates[[1]]
#> [1] 2.137777
#> 
#> $features[[5]]$geometry$coordinates[[2]]
#> [1] 41.68099
#> 
#> 
#> 
#> $features[[5]]$properties
#> $features[[5]]$properties$id
#> [1] 4392400
#> 
#> $features[[5]]$properties$url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/4392400.json"
#> 
#> $features[[5]]$properties$comment_url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/4392400/comment.json"
#> 
#> $features[[5]]$properties$close_url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/4392400/close.json"
#> 
#> $features[[5]]$properties$date_created
#> [1] "2024-08-19 20:06:00 UTC"
#> 
#> $features[[5]]$properties$status
#> [1] "open"
#> 
#> $features[[5]]$properties$comments
#> $features[[5]]$properties$comments[[1]]
#> $features[[5]]$properties$comments[[1]]$date
#> [1] "2024-08-19 20:06:00 UTC"
#> 
#> $features[[5]]$properties$comments[[1]]$uid
#> [1] 11725140
#> 
#> $features[[5]]$properties$comments[[1]]$user
#> [1] "jmaspons"
#> 
#> $features[[5]]$properties$comments[[1]]$user_url
#> [1] "https://api.openstreetmap.org/user/jmaspons"
#> 
#> $features[[5]]$properties$comments[[1]]$action
#> [1] "opened"
#> 
#> $features[[5]]$properties$comments[[1]]$text
#> [1] "Pista per cotxes al Fonoll\n\nvia StreetComplete 58.2\n\nGPS Trace: https://www.openstreetmap.org/user/jmaspons/traces/11432387\n"
#> 
#> $features[[5]]$properties$comments[[1]]$html
#> [1] "<p dir=\"auto\">Pista per cotxes al Fonoll</p>\n\n<p dir=\"auto\">via StreetComplete 58.2</p>\n\n<p dir=\"auto\">GPS Trace: <a href=\"https://www.openstreetmap.org/user/jmaspons/traces/11432387\" rel=\"nofollow noopener noreferrer\" dir=\"auto\">@jmaspons/traces/11432387</a>\n</p>"
#> 
#> 
#> 
#> 
#> 
#> $features[[6]]
#> $features[[6]]$type
#> [1] "Feature"
#> 
#> $features[[6]]$geometry
#> $features[[6]]$geometry$type
#> [1] "Point"
#> 
#> $features[[6]]$geometry$coordinates
#> $features[[6]]$geometry$coordinates[[1]]
#> [1] 1.887865
#> 
#> $features[[6]]$geometry$coordinates[[2]]
#> [1] 41.57131
#> 
#> 
#> 
#> $features[[6]]$properties
#> $features[[6]]$properties$id
#> [1] 2981309
#> 
#> $features[[6]]$properties$url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/2981309.json"
#> 
#> $features[[6]]$properties$comment_url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/2981309/comment.json"
#> 
#> $features[[6]]$properties$close_url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/2981309/close.json"
#> 
#> $features[[6]]$properties$date_created
#> [1] "2021-12-23 22:15:24 UTC"
#> 
#> $features[[6]]$properties$status
#> [1] "open"
#> 
#> $features[[6]]$properties$comments
#> $features[[6]]$properties$comments[[1]]
#> $features[[6]]$properties$comments[[1]]$date
#> [1] "2021-12-23 22:15:24 UTC"
#> 
#> $features[[6]]$properties$comments[[1]]$uid
#> [1] 11725140
#> 
#> $features[[6]]$properties$comments[[1]]$user
#> [1] "jmaspons"
#> 
#> $features[[6]]$properties$comments[[1]]$user_url
#> [1] "https://api.openstreetmap.org/user/jmaspons"
#> 
#> $features[[6]]$properties$comments[[1]]$action
#> [1] "opened"
#> 
#> $features[[6]]$properties$comments[[1]]$text
#> [1] "wikidata o wikipedia erronis? segons l'article de la wikipedia, és a https://geohack.toolforge.org/geohack.php?pagename=Les_Agulles_del_Petint%C3%B3&language=ca&params=41.6_N_1.9_E_"
#> 
#> $features[[6]]$properties$comments[[1]]$html
#> [1] "<p dir=\"auto\">wikidata o wikipedia erronis? segons l'article de la wikipedia, és a <a href=\"https://geohack.toolforge.org/geohack.php?pagename=Les_Agulles_del_Petint%C3%B3&amp;language=ca&amp;params=41.6_N_1.9_E_\" rel=\"nofollow noopener noreferrer\" dir=\"auto\">https://geohack.toolforge.org/geohack.php?pagename=Les_Agulles_del_Petint%C3%B3&amp;language=ca&amp;params=41.6_N_1.9_E_</a></p>"
#> 
#> 
#> 
#> 
#> 
#> $features[[7]]
#> $features[[7]]$type
#> [1] "Feature"
#> 
#> $features[[7]]$geometry
#> $features[[7]]$geometry$type
#> [1] "Point"
#> 
#> $features[[7]]$geometry$coordinates
#> $features[[7]]$geometry$coordinates[[1]]
#> [1] 2.230423
#> 
#> $features[[7]]$geometry$coordinates[[2]]
#> [1] 41.65313
#> 
#> 
#> 
#> $features[[7]]$properties
#> $features[[7]]$properties$id
#> [1] 2953547
#> 
#> $features[[7]]$properties$url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/2953547.json"
#> 
#> $features[[7]]$properties$comment_url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/2953547/comment.json"
#> 
#> $features[[7]]$properties$close_url
#> [1] "https://api.openstreetmap.org/api/0.6/notes/2953547/close.json"
#> 
#> $features[[7]]$properties$date_created
#> [1] "2021-11-29 12:28:13 UTC"
#> 
#> $features[[7]]$properties$status
#> [1] "open"
#> 
#> $features[[7]]$properties$comments
#> $features[[7]]$properties$comments[[1]]
#> $features[[7]]$properties$comments[[1]]$date
#> [1] "2021-11-29 12:28:13 UTC"
#> 
#> $features[[7]]$properties$comments[[1]]$action
#> [1] "opened"
#> 
#> $features[[7]]$properties$comments[[1]]$text
#> [1] "No es la Carretera de Bigues a Lliçà de Munt, el nom correcte és Carretera de Partes a Bigues"
#> 
#> $features[[7]]$properties$comments[[1]]$html
#> [1] "<p dir=\"auto\">No es la Carretera de Bigues a Lliçà de Munt, el nom correcte és Carretera de Partes a Bigues</p>"
#> 
#> 
#> $features[[7]]$properties$comments[[2]]
#> $features[[7]]$properties$comments[[2]]$date
#> [1] "2021-12-21 21:43:14 UTC"
#> 
#> $features[[7]]$properties$comments[[2]]$uid
#> [1] 11725140
#> 
#> $features[[7]]$properties$comments[[2]]$user
#> [1] "jmaspons"
#> 
#> $features[[7]]$properties$comments[[2]]$user_url
#> [1] "https://api.openstreetmap.org/user/jmaspons"
#> 
#> $features[[7]]$properties$comments[[2]]$action
#> [1] "commented"
#> 
#> $features[[7]]$properties$comments[[2]]$text
#> [1] "Tens alguna font? No hi ha cartells per comprovar-ho sobre el terreny"
#> 
#> $features[[7]]$properties$comments[[2]]$html
#> [1] "<p dir=\"auto\">Tens alguna font? No hi ha cartells per comprovar-ho sobre el terreny</p>"
#> 
#> 
#> 
#> 
#> 
#> 
```
