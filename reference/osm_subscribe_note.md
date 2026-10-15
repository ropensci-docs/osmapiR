# Subscribe or unsubscribe to a note

Subscribe or unsubscribe to a note

## Usage

``` r
osm_subscribe_note(note_id)

osm_unsubscribe_note(note_id)
```

## Arguments

- note_id:

  The id of the note represented by a numeric or a character value.

## Value

Returns nothing.

## Functions

- `osm_subscribe_note()`: Subscribe to the discussion of a note to
  receive notifications for new comments.

- `osm_unsubscribe_note()`: Unsubscribe from the discussion of a note to
  stop receiving notifications for new comments.

## Examples

``` r
if (FALSE) { # \dontrun{
# set_osmapi_connection(server = "openstreetmap.org")
osm_subscribe_note(2067786)
osm_unsubscribe_note("2067786")
} # }
```
