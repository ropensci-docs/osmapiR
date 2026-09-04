# Changelog

## osmapiR (development version)

## osmapiR 0.2.6

- Add mirrors <https://gitlab.com/jmaspons/osmapir> &
  <https://codeberg.org/jmaspons/osmapiR>
  ([\#75](https://github.com/ropensci/osmapiR/issues/75))
- Update documentation and code for server-side changes documented in
  OSMWikiVersion [2940426 -\>
  3068644](https://wiki.openstreetmap.org/w/index.php?title=API_v0.6&diff=3068644&oldid=2940426)
  ([\#86](https://github.com/ropensci/osmapiR/issues/86)).

## osmapiR 0.2.5

CRAN release: 2026-02-15

- Update documentation and code for server-side changes documented in
  OSMWikiVersion [2878437 -\>
  2940426](https://wiki.openstreetmap.org/w/index.php?title=API_v0.6&diff=2940426&oldid=2878437)
  ([\#72](https://github.com/ropensci/osmapiR/issues/72)).
  - Add new function
    [`osm_search_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_search_comment_changeset_discussion.md).
- `bbox` parameters now accepts more formats, including character,
  matrix, vector, `bbox` object from `sf` package, or a `SpatExtent`
  from `terra` package
  ([\#73](https://github.com/ropensci/osmapiR/issues/73)).

## osmapiR 0.2.4

CRAN release: 2025-08-18

- Fix for upcoming httr2 1.2.0 release
  ([\#67](https://github.com/ropensci/osmapiR/issues/67) by
  [@hadley](https://github.com/hadley)).
- Update documentation and code for server-side changes documented in
  OSMWikiVersion [2834473 -\>
  2878437](https://wiki.openstreetmap.org/w/index.php?title=API_v0.6&diff=2878437&oldid=2834473)
  ([\#69](https://github.com/ropensci/osmapiR/issues/69)).
  - Add `format = "json"` for
    [`osm_get_gpx_metadata()`](https://docs.ropensci.org/osmapiR/reference/osm_get_gpx_metadata.md).
  - New default for
    [`osm_search_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_search_notes.md)
    to `sort = "created_at"` instead of `sort = "updated_at"`.
- Rename internal functions for API endpoints from `osm_*` to `.osm_*`
  ([\#70](https://github.com/ropensci/osmapiR/issues/70)).

## osmapiR 0.2.3

CRAN release: 2025-04-15

- Update documentation and code for server-side changes documented in
  OSMWikiVersion [2775892 -\>
  2834473](https://wiki.openstreetmap.org/w/index.php?title=API_v0.6&diff=2834473&oldid=2775892)
  ([\#63](https://github.com/ropensci/osmapiR/issues/63)).
  - Update deprecated endpoints
  - Add new functions
    [`osm_subscribe_note()`](https://docs.ropensci.org/osmapiR/reference/osm_subscribe_note.md)
    and
    [`osm_unsubscribe_note()`](https://docs.ropensci.org/osmapiR/reference/osm_subscribe_note.md).
  - Add new functions
    [`osm_create_user_block()`](https://docs.ropensci.org/osmapiR/reference/osm_create_user_block.md),
    `osm_read_user_block()` and
    [`osm_list_active_user_blocks()`](https://docs.ropensci.org/osmapiR/reference/osm_list_active_user_blocks.md).
- Vectorized version of `osm_read_user_block()` -\>
  [`osm_get_user_blocks()`](https://docs.ropensci.org/osmapiR/reference/osm_get_user_blocks.md)
  ([\#65](https://github.com/ropensci/osmapiR/issues/65)).

## osmapiR 0.2.2

CRAN release: 2024-11-18

- Use the new function
  [`httr2::oauth_cache_clear()`](https://httr2.r-lib.org/reference/oauth_cache_clear.html)
  from httr2 1.0.6
  ([\#58](https://github.com/ropensci/osmapiR/issues/58) by
  [@hadley](https://github.com/hadley)).
- Update documentation and code for server-side changes documented in
  OSMWikiVersion [2711808 -\>
  2775892](https://wiki.openstreetmap.org/w/index.php?title=API_v0.6&diff=2775892&oldid=2711808)
  ([\#60](https://github.com/ropensci/osmapiR/issues/60)).
  - Add new parameters to `osm_query_changesets(..., from, to)`.
- Fix `osm_query_changesets(..., time, time_2)`
  ([\#61](https://github.com/ropensci/osmapiR/issues/61)).

## osmapiR 0.2.1

CRAN release: 2024-09-05

- Update CITATION with the JOSS article
  (<https://doi.org/10.21105/joss.07151>).
- Test and fix
  [`tags_list2wide()`](https://docs.ropensci.org/osmapiR/reference/tags_list-wide.md)
  with only 1 tag per object
  ([0368f1b](https://github.com/ropensci/osmapiR/commit/0368f1bf5ea9a0ba670d4dbd356846873460e96c)).

## osmapiR 0.2.0

*(published at <https://doi.org/10.5281/zenodo.13627998>)*

### New features

- Add `format = "sf"` for functions returning objects of class
  `osmapi_map_notes`
  ([\#36](https://github.com/ropensci/osmapiR/issues/36)).
- Add `format = "sf"` for functions returning objects of class
  `osmapi_changesets`
  ([\#37](https://github.com/ropensci/osmapiR/issues/37)).
- Add `format = "sf"` for
  [`osm_get_gpx_metadata()`](https://docs.ropensci.org/osmapiR/reference/osm_get_gpx_metadata.md)
  ([\#38](https://github.com/ropensci/osmapiR/issues/38)).
- Add `format = "sf"` for
  [`osm_list_gpxs()`](https://docs.ropensci.org/osmapiR/reference/osm_list_gpxs.md)
  ([\#42](https://github.com/ropensci/osmapiR/issues/42)).
- Add `format = "sf"` for functions returning objects of class
  `osmapi_gps_track`
  ([\#44](https://github.com/ropensci/osmapiR/issues/44)).
- Add `format = "sf"` for functions returning objects of class
  `osmapi_gpx` ([\#45](https://github.com/ropensci/osmapiR/issues/45)).
- Set encoding to UTF-8 for tags and user names in returned data.frames
  ([\#54](https://github.com/ropensci/osmapiR/issues/54)).
- Parse `<TrackPointExtension>` data from gpx if available
  ([\#49](https://github.com/ropensci/osmapiR/issues/49)).

### Minor improvements

- Upgrade logo by [@atarom](https://github.com/atarom).
- Add inst/CITATION.
- Updated links to the new osmapiR home at rOpenSci
  ([\#40](https://github.com/ropensci/osmapiR/issues/40)).
- Split functions to parse gpx data from different API endpoints and
  different properties
  ([\#43](https://github.com/ropensci/osmapiR/issues/43)).
- Implement NA bboxes in `st_as_sf.osmapi_chagesets()`
  ([7ea4f5d7](https://github.com/ropensci/osmapiR/commit/7ea4f5d7f412ef8cf7691741b836cf45ddeb61f2)).
- Remove dontrun in examples that don’t require authentication
  ([\#47](https://github.com/ropensci/osmapiR/issues/47)).
- Improve performance when parsing gpx data to data.frame
  ([\#48](https://github.com/ropensci/osmapiR/issues/48)).
- Tweaks in DESCRIPTION and CITATION files by
  [@Maelle](https://github.com/Maelle)
  ([\#50](https://github.com/ropensci/osmapiR/issues/50),
  [\#51](https://github.com/ropensci/osmapiR/issues/51)).
- Sort OSM objects in `osm_get_objects(..., full_objects = TRUE)` and
  optimize ([\#52](https://github.com/ropensci/osmapiR/issues/52)).

### Bug fixes

- Improve tests and fix bugs
  ([\#35](https://github.com/ropensci/osmapiR/issues/35),
  [08fb4b1](https://github.com/ropensci/osmapiR/commit/08fb4b10abf0270d8bea2473b02b2520ba341521)).
- Fix miscalculation of the nchar_url that trigger errors when many ids
  are requested in `osm_fetch_objects()`.
- Fix changesets’ bbox in `st_as_sf.osmapi_chagesets()`
  ([84f16e7a](https://github.com/ropensci/osmapiR/commit/84f16e7adda087ab707cc2644c79ff1590cf307e)).

## osmapiR 0.1.0

CRAN release: 2024-06-28

- Initial CRAN submission implementing calls to all the API endpoints.
- Server responses are returned as R objects, xml_documents or json
  lists.
- Authentication when needed with OAuth2.
- Pagination in server responses handled internally
  ([\#20](https://github.com/ropensci/osmapiR/issues/20),
  [\#23](https://github.com/ropensci/osmapiR/issues/23) &
  [\#29](https://github.com/ropensci/osmapiR/issues/29)).
- Vectorization of atomic API calls
  ([\#18](https://github.com/ropensci/osmapiR/issues/18)).
