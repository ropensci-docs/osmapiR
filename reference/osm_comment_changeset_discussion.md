# Comment a changeset

Add a comment to a changeset and subscribe to the discussion. The
changeset must be closed. Requires authentication.

## Usage

``` r
osm_comment_changeset_discussion(changeset_id, comment)
```

## Arguments

- changeset_id:

  The id of the changeset to comment represented by a numeric or a
  character value.

- comment:

  The text of the comment to post.

## Value

Returns a data frame with the changeset (same format as
[`osm_get_changesets()`](https://docs.ropensci.org/osmapiR/reference/osm_get_changesets.md)
with `format = "R"`).

## Note

Requires either `write_api` or `write_changeset_comments` OAuth scope.

## See also

Other changeset discussion's functions:
[`osm_hide_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_hide_comment_changeset_discussion.md),
[`osm_search_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_search_comment_changeset_discussion.md),
[`osm_subscribe_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_subscribe_changeset_discussion.md)

## Examples

``` r
if (FALSE) { # \dontrun{
set_osmapi_connection("testing") # use the testing server
changeset <- osm_get_changesets(300626)
updated_changeset <- osm_comment_changeset_discussion(
  changeset_id = changeset$id,
  comment = "A new comment to test osmapiR"
)
updated_changeset
} # }
```
