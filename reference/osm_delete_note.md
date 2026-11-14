# Delete notes

Hide (delete) notes. This request needs to be done as an authenticated
user with moderator role.

## Usage

``` r
osm_delete_note(note_id, text)
```

## Arguments

- note_id:

  Note ids represented by a numeric or a character vector.

- text:

  A non-mandatory comment as text.

## Value

Returns a data frame with the hided map notes (same format as
[`osm_get_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_get_notes.md)
with `format = "R"`).

## Details

Use
[`osm_reopen_note()`](https://docs.ropensci.org/osmapiR/reference/osm_close_note.md)
to make the note visible again.

## See also

Other edit notes' functions:
[`osm_close_note()`](https://docs.ropensci.org/osmapiR/reference/osm_close_note.md),
[`osm_create_comment_note()`](https://docs.ropensci.org/osmapiR/reference/osm_create_comment_note.md),
[`osm_create_note()`](https://docs.ropensci.org/osmapiR/reference/osm_create_note.md)

Other functions for moderators:
[`osm_create_user_block()`](https://docs.ropensci.org/osmapiR/reference/osm_create_user_block.md),
[`osm_hide_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_hide_comment_changeset_discussion.md),
[`osm_redaction_object()`](https://docs.ropensci.org/osmapiR/reference/osm_redaction_object.md)

## Examples

``` r
if (FALSE) { # \dontrun{
set_osmapi_connection("testing") # use the testing server
note <- osm_create_note(lat = "40.7327375", lon = "0.1702526", text = "Test note to delete.")
del_note <- osm_delete_note(note_id = note$id, text = "Hide note")
del_note
} # }
```
