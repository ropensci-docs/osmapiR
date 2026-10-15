# Create, update, or close a changeset

Create, update, or close a changeset

## Usage

``` r
osm_create_changeset(
  comment,
  ...,
  created_by = paste("osmapiR", getOption("osmapir.osmapir_version")),
  verbose = FALSE
)

osm_update_changeset(
  changeset_id,
  comment,
  ...,
  created_by = paste("osmapiR", getOption("osmapir.osmapir_version")),
  verbose = FALSE
)

osm_close_changeset(changeset_id)
```

## Arguments

- comment:

  Tag comment is mandatory.

- ...:

  Arbitrary tags to add to the changeset as named parameters (key =
  "value").

- created_by:

  Tag with the client data. By default, `osmapiR x.y.z`.

- verbose:

  If `TRUE`, print the tags of the new changeset.

- changeset_id:

  The id of the changeset to update. The user issuing this API call has
  to be the same that created the changeset.

## Value

The ID of the newly created changeset or a `data.frame` inheriting
`osmapi_changesets` with the details of the updated changeset.

Nothing is returned upon successful closing of a changeset.

## Details

See <https://wiki.openstreetmap.org/wiki/Changeset> for details and the
most common changeset's tags.

When updating a changeset, unchanged tags have to be repeated in order
to not be deleted.

## Functions

- `osm_create_changeset()`: Open a new changeset for editing.

- `osm_update_changeset()`: Update the tags of an open changeset.

- `osm_close_changeset()`: Close a changeset. A changeset may already
  have been closed without the owner issuing this API call. In this case
  an error code is returned.

## See also

Other edit changeset's functions:
[`osm_diff_upload_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_diff_upload_changeset.md)

## Examples

``` r
if (FALSE) { # \dontrun{
set_osmapi_connection("testing") # use the testing server

chset_id <- osm_create_changeset(
  comment = "Describe the changeset",
  source = "GPS;survey",
  hashtags = "#testing;#osmapiR"
)

chaset <- osm_get_changesets(changeset_id = chset_id)
chaset

upd_chaset <- osm_update_changeset(
  changeset_id = chset_id,
  comment = "Improved description of the changeset",
  hashtags = "#testing;#osmapiR"
)
upd_chaset
} # }
```
