# Create a new note

Create a new note

## Usage

``` r
osm_create_note(lat, lon, text, authenticate = TRUE)
```

## Arguments

- lat:

  Specifies the latitude in decimal degrees of the note.

- lon:

  Specifies the longitude in decimal degrees of the note.

- text:

  A text field with arbitrary text containing the note.

- authenticate:

  If `TRUE` (default), the note is authored by the logged user.
  Otherwise, anonymous note.

## Value

Returns a data frame with the map note (same format as
[`osm_get_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_get_notes.md)
with `format = "R"`).

## Details

If the request is made as an authenticated user, the note is associated
to that user account. If the OAuth access token used does not have the
`allow_write_notes` permission, it is created as an anonymous note
instead.

## See also

Other edit notes' functions:
[`osm_close_note()`](https://docs.ropensci.org/osmapiR/reference/osm_close_note.md),
[`osm_create_comment_note()`](https://docs.ropensci.org/osmapiR/reference/osm_create_comment_note.md),
[`osm_delete_note()`](https://docs.ropensci.org/osmapiR/reference/osm_delete_note.md)

## Examples

``` r
if (FALSE) { # \dontrun{
set_osmapi_connection("testing") # use the testing server
new_note <- osm_create_note(lat = 41.38373, lon = 2.18233, text = "Testing osmapiR")
new_note
} # }
```
