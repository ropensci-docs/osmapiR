# Authenticate or logout osmapiR

Log in/out osmapiR.

## Usage

``` r
authenticate_osmapi()

logout_osmapi()
```

## Value

For `authenticate_osmapi`, print the user and permissions of the
connection and return invisibly the display name of the logged user.
`logout_osmapi` clear the OAuth2 token and can be useful to change user.

## Details

All functions that require authentication will trigger the log in if the
session is not yet authenticated, so calling this function is not really
needed. Use `authenticate_osmapi` to sign in before executing scripts
that require authentication to avoid interruptions.

## See also

Other API functions:
[`osm_api_versions()`](https://docs.ropensci.org/osmapiR/reference/osm_api_versions.md),
[`osm_capabilities()`](https://docs.ropensci.org/osmapiR/reference/osm_capabilities.md),
[`osm_permissions()`](https://docs.ropensci.org/osmapiR/reference/osm_permissions.md),
[`set_osmapi_connection()`](https://docs.ropensci.org/osmapiR/reference/API_configuration.md)

## Examples

``` r
if (FALSE) { # \dontrun{
authenticate_osmapi()
logout_osmapi()
} # }
```
