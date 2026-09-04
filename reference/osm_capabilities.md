# Capabilities of the API

Provide information about the capabilities and limitations of the
current API.

## Usage

``` r
osm_capabilities()
```

## Value

A list with the API capabilities and policies.

## Details

API:

- `version` `minimum` and `maximum` are the API call versions that the
  server will accept.

- `area` `maximum` is the maximum area in square degrees that can be
  queried by API calls.

- `note_area` `maximum` is the maximum area in square degrees that can
  be queried for notes by API calls.

- `tracepoints` `per_page` is the maximum number of GPS trace points
  returned at once by an API call. This value defines the page size.

- `waynodes` `maximum` is the maximum number of nodes that a way may
  contain.

- `relationmember` `maximum` is the maximum number of members that a
  relation may contain.

- `changesets` `maximum_elements` is the maximum number of combined
  nodes, ways and relations that can be contained in a changeset.

- `changesets` `default_query_limit` and `maximum_query_limit` are the
  default and maximum values of the limit parameter of
  [`osm_query_changesets()`](https://docs.ropensci.org/osmapiR/reference/osm_query_changesets.md).

- `notes` `default_query_limit` and `maximum_query_limit` are the
  default and maximum values of the limit parameter of notes bounding
  box queries
  ([`osm_read_bbox_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_read_bbox_notes.md))
  and search
  ([`osm_search_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_search_notes.md)).

- The `status` element returns either *online*, *readonly* or *offline*
  for each of the database, API and GPX API. The `database` field is
  informational, and the `API`/`GPX-API` fields indicate whether a
  client should expect read and write requests to work (*online*), only
  read requests to work (*readonly*) or no requests to work (*offline*).

Policy:

- Imagery blacklist lists all aerial and map sources, which are not
  permitted for OSM usage due to copyright. Editors must not show these
  resources as background layer.

## See also

Other API functions:
[`authenticate_osmapi()`](https://docs.ropensci.org/osmapiR/reference/authenticate_osmapiR.md),
[`osm_api_versions()`](https://docs.ropensci.org/osmapiR/reference/osm_api_versions.md),
[`osm_permissions()`](https://docs.ropensci.org/osmapiR/reference/osm_permissions.md),
[`set_osmapi_connection()`](https://docs.ropensci.org/osmapiR/reference/API_configuration.md)

## Examples

``` r
osm_capabilities()
#> $api
#> $api$version
#> minimum maximum 
#>   "0.6"   "0.6" 
#> 
#> $api$area
#> maximum 
#>    0.25 
#> 
#> $api$note_area
#> maximum 
#>      25 
#> 
#> $api$tracepoints
#> per_page 
#>     5000 
#> 
#> $api$waynodes
#> maximum 
#>    2000 
#> 
#> $api$relationmembers
#> maximum 
#>   32000 
#> 
#> $api$changesets
#>    maximum_elements default_query_limit maximum_query_limit 
#>               10000                 100                 100 
#> 
#> $api$notes
#> default_query_limit maximum_query_limit 
#>                 100               10000 
#> 
#> $api$timeout
#> seconds 
#>     300 
#> 
#> $api$status
#> database      api      gpx 
#> "online" "online" "online" 
#> 
#> 
#> $policy
#> $policy$imagery
#> $policy$imagery[[1]]
#>                    blacklist 
#> ".*\\.google(apis)?\\..*/.*" 
#> 
#> $policy$imagery[[2]]
#>                              blacklist 
#> "https?://xdworld\\.vworld\\.kr[/:].*" 
#> 
#> $policy$imagery[[3]]
#>               blacklist 
#> ".*\\.here\\.com[/:].*" 
#> 
#> $policy$imagery[[4]]
#>          blacklist 
#> ".*\\.mapy\\.cz.*" 
#> 
#> $policy$imagery[[5]]
#>                        blacklist 
#> ".*\\.api-maps\\.yandex\\.ru/.*" 
#> 
#> $policy$imagery[[6]]
#>                     blacklist 
#> ".*\\.maps\\.yandex\\.net/.*" 
#> 
#> $policy$imagery[[7]]
#>                   blacklist 
#> ".*\\.maps\\.2gis\\.com/.*" 
#> 
#> 
#> 
```
