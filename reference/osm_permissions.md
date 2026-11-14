# Retrieving permissions

Returns the permissions granted to the current API connection.

## Usage

``` r
osm_permissions(format = c("R", "xml", "json"))
```

## Arguments

- format:

  Format of the output. Can be `"R"` (default), `"xml"`, or `"json"`.

## Value

If the API client is not authorized, an empty list of permissions will
be returned. Otherwise, the list will be based on the granted scopes of
the logged user.

## Details

Currently the following permissions can appear in the result,
corresponding directly to the ones used in the OAuth 2.0 application
definition:

- allow_read_prefs (read user preferences)

- allow_write_prefs (modify user preferences)

- allow_write_diary (create diary entries, comments and make friends)

- allow_write_api (modify the map)

- allow_write_changeset_comments

- allow_write_redactions (redact element versions)

- allow_read_gpx (read private GPS traces)

- allow_write_gpx (upload GPS traces)

- allow_write_notes (modify notes)

- allow_write_redactions (redact map data)

- allow_write_blocks (create and revoke user blocks)

- allow_consume_messages (read, update status and delete user messages)

- allow_send_messages (send private messages to other users)

## Note

For compatibility reasons, all OAuth 2.0 scopes will be prefixed by
"allow\_", e.g. scope "read_prefs" will be shown as permission
"allow_read_prefs".

## See also

Other API functions:
[`authenticate_osmapi()`](https://docs.ropensci.org/osmapiR/reference/authenticate_osmapiR.md),
[`osm_api_versions()`](https://docs.ropensci.org/osmapiR/reference/osm_api_versions.md),
[`osm_capabilities()`](https://docs.ropensci.org/osmapiR/reference/osm_capabilities.md),
[`set_osmapi_connection()`](https://docs.ropensci.org/osmapiR/reference/API_configuration.md)

## Examples

``` r
if (FALSE) { # \dontrun{
perms <- osm_permissions()
perms
} # }
```
