# Create a new comment in a note

Add a new comment to an existing note. Requires authentication.

## Usage

``` r
osm_create_comment_note(note_id, text)
```

## Arguments

- note_id:

  Note id represented by a numeric or a character value.

- text:

  The comment as arbitrary text.

## Value

Returns a data frame with the map note and the new comment (same format
as
[`osm_get_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_get_notes.md)
with `format = "R"`).

## See also

Other edit notes' functions:
[`osm_close_note()`](https://docs.ropensci.org/osmapiR/reference/osm_close_note.md),
[`osm_create_note()`](https://docs.ropensci.org/osmapiR/reference/osm_create_note.md),
[`osm_delete_note()`](https://docs.ropensci.org/osmapiR/reference/osm_delete_note.md)

## Examples

``` r
if (FALSE) { # \dontrun{
set_osmapi_connection("testing") # use the testing server
note <- osm_get_notes(53726)
updated_note <- osm_create_comment_note(note$id, text = "A new comment to the note")
updated_note
} # }
```
