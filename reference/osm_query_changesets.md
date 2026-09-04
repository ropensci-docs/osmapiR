# Query changesets

This is an API method for querying changesets. It supports querying by
different criteria.

## Usage

``` r
osm_query_changesets(
  bbox,
  user,
  time,
  time_2,
  from,
  to,
  open,
  closed,
  changeset_ids,
  order = c("newest", "oldest"),
  limit = getOption("osmapir.api_capabilities")$api$changesets["default_query_limit"],
  format = c("R", "sf", "xml", "json"),
  tags_in_columns = FALSE
)
```

## Arguments

- bbox:

  Find changesets within the given bounding box coordinates
  (`left,bottom,right,top`). It can be specified by a character, matrix,
  vector, `bbox` object from sf, a `SpatExtent` from terra. Unnamed
  vectors and matrices will be sorted appropriately and must merely be
  in the order (`x`, `y`, `x`, `y`) or `x` in the first column and `y`
  in the second column.

- user:

  Find changesets by the user with the given user id (numeric) or
  display name (character).

- time:

  Find changesets **closed** after this date and time. See details for
  the valid formats.

- time_2:

  find changesets that were **closed** after `time` and **created**
  before `time_2`. In other words, any changesets that were open **at
  some time** during the given time range `time` to `time_2`. See
  details for the valid formats.

- from:

  Find changesets **created** at or after this value. See details for
  the valid formats.

- to:

  Find changesets **created** before this value. `to` requires `from`,
  but not vice-versa. If `to` is provided alone, it has no effect. See
  details for the valid formats.

- open:

  If `TRUE`, only finds changesets that are still **open** but excludes
  changesets that are closed or have reached the element limit for a
  changeset (10,000 at the moment `osm_capabilities()$api$changesets`).

- closed:

  If `TRUE`, only finds changesets that are **closed** or have reached
  the element limit.

- changeset_ids:

  Finds changesets with the specified ids.

- order:

  If `"newest"` (default), sort newest changesets first. If `"oldest"`,
  reverse order.

- limit:

  Specifies the maximum number of changesets returned. 100 as the
  default value.

- format:

  Format of the output. Can be `"R"` (default), `"sf"`, `"xml"`, or
  `"json"`.

- tags_in_columns:

  If `FALSE` (default), the tags of the changesets are saved in a single
  list column `tags` containing a `data.frame` for each changeset with
  the keys and values. If `TRUE`, add a column for each key. Ignored if
  `format != "R"`.

## Value

If `format = "R"`, returns a data frame with one OSM changeset per row.
If `format = "sf"`, returns a `sf` object from sf.

### `format = "xml"`

Returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) with
the following format:

    <osm version="0.6" generator="OpenStreetMap server" copyright="OpenStreetMap and contributors" attribution="http://www.openstreetmap.org/copyright" license="http://opendatacommons.org/licenses/odbl/1-0/">
      <changeset id="10" created_at="2005-05-01T16:09:37Z" open="false" comments_count="1" changes_count="10" closed_at="2005-05-01T17:16:44Z" min_lat="59.9513092" min_lon="10.7719727" max_lat="59.9561501" max_lon="10.7994537" uid="24" user="Petter Reinholdtsen">
        <tag k="created_by" v="JOSM 1.61"/>
        <tag k="comment" v="Just adding some streetnames"/>
        ...
      </changeset>
      <changeset ...>
        ...
      </changeset>
    </osm>

### `format = "json"`

*Please note that the JSON format has changed on August 25, 2024 with
the release of openstreetmap-cgimap 2.0.0, to* *align it with the
existing Rails format.*

Returns a list with the following json structure:

    {
      "version": "0.6",
      "generator": "openstreetmap-cgimap 2.0.0 (4003517 spike-08.openstreetmap.org)",
      "copyright": "OpenStreetMap and contributors",
      "attribution": "http://www.openstreetmap.org/copyright",
      "license": "http://opendatacommons.org/licenses/odbl/1-0/",
      "changesets": [
        {
          "id": 10,
          "created_at": "2005-05-01T16:09:37Z",
          "open": false,
          "comments_count": 1,
          "changes_count": 10,
          "closed_at": "2005-05-01T17:16:44Z",
          "min_lat": 59.9513092,
          "min_lon": 10.7719727,
          "max_lat": 59.9561501,
          "max_lon": 10.7994537,
          "uid": 24,
          "user": "Petter Reinholdtsen",
          "tags": {
              "comment": "Just adding some streetnames",
              "created_by": "JOSM 1.61"
          }
        },
        ...
      ]
    }

## Details

Where multiple queries are given the result will be those which match
all of the requirements. The contents of the returned document are the
changesets and their tags. To get the full set of changes associated
with a changeset, use
[`osm_download_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_download_changeset.md)
on each changeset ID individually.

Modification and extension of the basic queries above may be required to
support rollback and other uses we find for changesets.

This call returns latest changesets matching criteria. The default
ordering is newest first, but you can specify `order = "oldest"` to
reverse the sort order (see [ordered by
`created_at`](https://github.com/openstreetmap/openstreetmap-website/blob/f1c6a87aa137c11d0aff5a4b0e563ac2c2a8f82d/app/controllers/api/changesets_controller.rb#L174)
– see the [current
state](https://github.com/openstreetmap/openstreetmap-website/blob/master/app/controllers/api/changesets_controller.rb#L174)).
Reverse ordering cannot be combined with `time`.

Te valid formats for `time`, `time_2`, `from` and `to` parameters are
[POSIXt](https://rdrr.io/r/base/DateTimeClasses.html) values or
characters with anything that [`Time.parse` Ruby
function](https://ruby-doc.org/stdlib-2.7.0/libdoc/time/rdoc/Time.html#method-c-parse)
will parse.

## See also

Other get changesets' functions:
[`osm_download_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_download_changeset.md),
[`osm_get_changesets()`](https://docs.ropensci.org/osmapiR/reference/osm_get_changesets.md)

## Examples

``` r
chst_ids <- osm_query_changesets(changeset_ids = c(137627129, 137625624))
chst_ids
#>          id          created_at           closed_at  open               user
#> 1 137627129 2023-06-22 02:23:23 2023-06-22 02:23:24 FALSE Mementomoristultus
#> 2 137625624 2023-06-22 00:38:20 2023-06-22 00:38:20 FALSE Mementomoristultus
#>        uid    min_lat    min_lon    max_lat    max_lon comments_count
#> 1 19648429 39.8308943  4.1564704 40.0215358  4.3280260              0
#> 2 19648429 42.2050642 -7.7351732 42.2050642 -7.7351732              0
#>   changes_count
#> 1             2
#> 2             1
#>                                                                                  tags
#> 1 6 tags: changesets_count=154 | comment=--- | created_by=iD 2.25.2 | host=https:/...
#> 2 6 tags: changesets_count=53 | comment=A ver, subnormal, en español es JUNUQUERA ...

chsts <- osm_query_changesets(
  bbox = c(2.65, 42.68, 2.71, 42.69),
  user = 19641470,
  time = "2023-06-20",
  time_2 = "2023-06-22",
  tags_in_columns = TRUE
)
chsts
#>          id          created_at           closed_at  open      user      uid
#> 1 137595351 2023-06-21 09:09:18 2023-06-21 09:09:18 FALSE Quercinus 19641470
#>      min_lat   min_lon    max_lat   max_lon comments_count changes_count
#> 1 42.6799619 2.6580564 42.6936802 2.7125775              4             1
#>   changesets_count                                              comment
#> 1                1 Correcció d'acord amb la toponímia oficial en català
#>   created_by                               host   ideditor:walkthrough_progress
#> 1  iD 2.25.2 https://www.openstreetmap.org/edit welcome;point;line;startEditing
#>   ideditor:walkthrough_started imagery_used locale
#> 1                          yes  BDOrtho IGN     ca

chsts2 <- osm_query_changesets(
  bbox = c("-9.3015367,41.8073642,-6.7339533,43.790422"),
  user = "Mementomoristultus",
  closed = "true"
)
head(chsts2)
#>          id          created_at           closed_at  open               user
#> 1 137626978 2023-06-22 02:10:24 2023-06-22 02:10:24 FALSE Mementomoristultus
#> 2 137626972 2023-06-22 02:09:43 2023-06-22 02:09:44 FALSE Mementomoristultus
#> 3 137626970 2023-06-22 02:09:28 2023-06-22 02:09:28 FALSE Mementomoristultus
#> 4 137626862 2023-06-22 02:01:25 2023-06-22 02:01:26 FALSE Mementomoristultus
#> 5 137626853 2023-06-22 02:00:48 2023-06-22 02:00:48 FALSE Mementomoristultus
#> 6 137626849 2023-06-22 02:00:24 2023-06-22 02:00:24 FALSE Mementomoristultus
#>        uid    min_lat    min_lon    max_lat    max_lon comments_count
#> 1 19648429 42.4327433 -6.9782486 42.4328559 -6.9780026              0
#> 2 19648429 42.4327498 -6.9765097 42.4328834 -6.9763031              0
#> 3 19648429 42.4328903 -6.9756364 42.4330040 -6.9754741              0
#> 4 19648429 43.4488066 -7.8527610 43.4501613 -7.8507456              0
#> 5 19648429 43.4499647 -7.8526224 43.4500774 -7.8525214              0
#> 6 19648429 43.4498605 -7.8527232 43.4509926 -7.8497643              0
#>   changes_count
#> 1             5
#> 2             5
#> 3             5
#> 4             2
#> 5             1
#> 6             7
#>                                                                                  tags
#> 1 6 tags: changesets_count=150 | comment=18945 | created_by=iD 2.25.2 | host=https...
#> 2 6 tags: changesets_count=149 | comment=18945 | created_by=iD 2.25.2 | host=https...
#> 3 6 tags: changesets_count=148 | comment=18945 | created_by=iD 2.25.2 | host=https...
#> 4 6 tags: changesets_count=144 | comment=11 | created_by=iD 2.25.2 | host=https://...
#> 5 6 tags: changesets_count=143 | comment=13 | created_by=iD 2.25.2 | host=https://...
#> 6 6 tags: changesets_count=142 | comment=13 | created_by=iD 2.25.2 | host=https://...
```
