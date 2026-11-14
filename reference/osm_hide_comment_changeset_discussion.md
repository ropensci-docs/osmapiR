# Hide or unhide a changeset comment

This request needs to be done as an authenticated user with moderator
role.

## Usage

``` r
osm_hide_comment_changeset_discussion(comment_id)

osm_unhide_comment_changeset_discussion(comment_id)
```

## Arguments

- comment_id:

  Note that the changeset comment id differs from the changeset id.

## Value

Returns a data frame with the changeset (same format as
[`osm_get_changesets()`](https://docs.ropensci.org/osmapiR/reference/osm_get_changesets.md)
with `format = "R"`).

## Functions

- `osm_hide_comment_changeset_discussion()`: Sets visible flag on
  changeset comment to false.

- `osm_unhide_comment_changeset_discussion()`: Sets visible flag on
  changeset comment to true.

## See also

Other changeset discussion's functions:
[`osm_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_comment_changeset_discussion.md),
[`osm_search_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_search_comment_changeset_discussion.md),
[`osm_subscribe_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_subscribe_changeset_discussion.md)

Other functions for moderators:
[`osm_create_user_block()`](https://docs.ropensci.org/osmapiR/reference/osm_create_user_block.md),
[`osm_delete_note()`](https://docs.ropensci.org/osmapiR/reference/osm_delete_note.md),
[`osm_redaction_object()`](https://docs.ropensci.org/osmapiR/reference/osm_redaction_object.md)

## Examples

``` r
if (FALSE) { # \dontrun{
chdis <- osm_get_changesets("265646", include_discussion = TRUE)
hide_com <- osm_hide_comment_changeset_discussion(comment_id = chdis$discussion[[1]]$id[1])
unhide_com <- osm_unhide_comment_changeset_discussion(comment_id = chdis$discussion[[1]]$id[1])
} # }
```
