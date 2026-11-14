# Create a user block

Create a user block

## Usage

``` r
osm_create_user_block(
  user_id,
  reason,
  period,
  needs_view = FALSE,
  format = c("R", "xml", "json")
)
```

## Arguments

- user_id:

  Blocked user id.

- reason:

  Reason for block shown to the blocked user (markdown text).

- period:

  Block duration in hours between 0 and maximum block period, currently
  87660.

- needs_view:

  If `TRUE`, the user is required to view the block page for the block
  to be lifted. Default to `FALSE`.

- format:

  Format of the output. Can be `"R"` (default), `"xml"`, or `"json"`.

## Value

Same format as
[`osm_get_user_blocks()`](https://docs.ropensci.org/osmapiR/reference/osm_get_user_blocks.md)

## See also

Other user blocks' functions:
[`osm_get_user_blocks()`](https://docs.ropensci.org/osmapiR/reference/osm_get_user_blocks.md),
[`osm_list_active_user_blocks()`](https://docs.ropensci.org/osmapiR/reference/osm_list_active_user_blocks.md)

Other functions for moderators:
[`osm_delete_note()`](https://docs.ropensci.org/osmapiR/reference/osm_delete_note.md),
[`osm_hide_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_hide_comment_changeset_discussion.md),
[`osm_redaction_object()`](https://docs.ropensci.org/osmapiR/reference/osm_redaction_object.md)

## Examples

``` r
if (FALSE) { # \dontrun{
set_osmapi_connection("testing") # use the testing server

my_user_id <- osm_details_logged_user()$user["id"]
osm_create_user_block(user_id = my_user_id, reason = "Not really evil, just testing.", period = 0)
} # }
```
