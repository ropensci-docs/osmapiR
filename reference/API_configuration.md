# Configure connections from osmapiR

Functions to configure the connections. Probably, you should only use
`set_osmapi_connection`.

## Usage

``` r
set_osmapi_connection(
  server = c("openstreetmap.org", "testing"),
  cache_authentication
)

get_osmapi_url()

set_osmapi_url(osmapi_url)
```

## Arguments

- server:

  If `openstreetmap.org` (default), the API calls will be performed to
  the servers in production. If `testing`, the calls will be against
  <https://master.apis.dev.openstreetmap.org> without affecting the main
  OSM data.

- cache_authentication:

  If `TRUE`, the authentication token will be cached on disk. This
  reduces the number of times that you need to re-authenticate at the
  cost of storing access credentials on disk. Cached tokens are
  encrypted and automatically deleted 30 days after creation. If missing
  (default), no changes will be applied. On package load time, the
  option is set to `FALSE` if it's not yet set.

- osmapi_url:

  The desired API URL to send the calls.

## Value

Configure
`.Options[grep("^osmapir\\.[a-z]+_(?!secret$)", names(.Options), perl = TRUE)]`
:) and return `osmapir.base_api_url`.

## Details

When testing your software against the API you should consider using
<https://master.apis.dev.openstreetmap.org> instead of the live-api
(`set_osmapi_connection("testing")`). Your account for the live service
is not in the same database, so you probably need a new username and
password for the test service; please visit that page in a browser to
sign up.

`set_osmapi_url()` and `get_osmapi_url` only deal with the API base URL.
On the other hand, `set_osmapi_connection` also configure the
authentication parameters needed for `PUT`, `POST` and `DELETE` calls.

For further details, see <https://wiki.openstreetmap.org/wiki/API_v0.6>.

## See also

Other API functions:
[`authenticate_osmapi()`](https://docs.ropensci.org/osmapiR/reference/authenticate_osmapiR.md),
[`osm_api_versions()`](https://docs.ropensci.org/osmapiR/reference/osm_api_versions.md),
[`osm_capabilities()`](https://docs.ropensci.org/osmapiR/reference/osm_capabilities.md),
[`osm_permissions()`](https://docs.ropensci.org/osmapiR/reference/osm_permissions.md)

## Examples

``` r
ori <- get_osmapi_url()
set_osmapi_connection(server = "testing")
#> Logged out from https://api.openstreetmap.org
get_osmapi_url()
#> [1] "https://master.apis.dev.openstreetmap.org"
set_osmapi_connection(server = "openstreetmap.org")
#> Logged out from https://master.apis.dev.openstreetmap.org
get_osmapi_url()
#> [1] "https://api.openstreetmap.org"

## Restore options
if (ori == "https://api.openstreetmap.org") {
  set_osmapi_connection(server = "openstreetmap.org")
} else if (ori == "https://master.apis.dev.openstreetmap.org") {
  set_osmapi_connection(server = "testing")
} else {
  warning(
    "A non standard osmapiR connection detected (", ori,
    "). If you configured manually options like \"osmapir.base_api_url\" or \"osmapir.oauth_id\", ",
    "configure it again."
  )
}
```
