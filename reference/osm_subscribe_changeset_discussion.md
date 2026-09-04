# Subscribe or unsubscribe to a changeset discussion

Subscribe or unsubscribe to a changeset discussion

## Usage

``` r
osm_subscribe_changeset_discussion(changeset_id)

osm_unsubscribe_changeset_discussion(changeset_id)
```

## Arguments

- changeset_id:

  The id of the changeset represented by a numeric or a character value.

## Value

Returns the changeset information.

## Functions

- `osm_subscribe_changeset_discussion()`: Subscribe to the discussion of
  a changeset to receive notifications for new comments.

- `osm_unsubscribe_changeset_discussion()`: Unsubscribe from the
  discussion of a changeset to stop receiving notifications.

## See also

Other changeset discussion's functions:
[`osm_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_comment_changeset_discussion.md),
[`osm_hide_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_hide_comment_changeset_discussion.md),
[`osm_search_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_search_comment_changeset_discussion.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# set_osmapi_connection(server = "openstreetmap.org")
osm_subscribe_changeset_discussion(137595351)
osm_unsubscribe_changeset_discussion("137595351")
} # }
```
