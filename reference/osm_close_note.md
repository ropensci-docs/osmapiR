# Close or reopen notes

Requires authentication.

## Usage

``` r
osm_close_note(note_id)

osm_reopen_note(note_id)
```

## Arguments

- note_id:

  Note ids represented by a numeric or character vector.

## Value

Returns a data frame with the closed map notes (same format as
[`osm_get_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_get_notes.md)
with `format = "R"`).

## Functions

- `osm_close_note()`: Close notes as fixed.

- `osm_reopen_note()`: Reopen closed notes.

## See also

Other edit notes' functions:
[`osm_create_comment_note()`](https://docs.ropensci.org/osmapiR/reference/osm_create_comment_note.md),
[`osm_create_note()`](https://docs.ropensci.org/osmapiR/reference/osm_create_note.md),
[`osm_delete_note()`](https://docs.ropensci.org/osmapiR/reference/osm_delete_note.md)

## Examples

``` r
if (FALSE) { # \dontrun{
set_osmapi_connection("testing") # use the testing server
note <- osm_create_note(lat = 41.38373, lon = 2.18233, text = "Testing osmapiR")
closed_note <- osm_close_note(note$id)
closed_note
reopened_note <- osm_reopen_note(note$id)
reopened_note
closed_note <- osm_close_note(note$id) # leave it closed
} # }
```
