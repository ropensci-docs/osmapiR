# Redact an object version

Used by the [Data Working
Group](https://wiki.openstreetmap.org/wiki/Data_working_group) to hide
old versions of elements containing data privacy or copyright
infringements. Only permitted for OSM accounts with the moderator role
(DWG and server admins).

## Usage

``` r
osm_redaction_object(
  osm_type = c("node", "way", "relation"),
  osm_id,
  version,
  redaction_id
)
```

## Arguments

- osm_type:

  Object type (`"node"`, `"way"` or `"relation"`).

- osm_id:

  Object id represented by a numeric or a character value.

- version:

  Version of the object to redact.

- redaction_id:

  If missing, then this is an unredact operation. If a redaction ID was
  specified, then set this element to be redacted in that redaction.

## Value

Nothing is returned upon successful redaction or unredaction of an
object.

## Details

The `redaction_id` is listed on
<https://www.openstreetmap.org/redactions>. More information can be
found in [the
source](https://git.openstreetmap.org/rails.git/blob/HEAD:/app/controllers/redactions_controller.rb).

## Note

Requires `write_redactions` OAuth scope; before September 2024 required
either `write_api` or `write_redactions`, and before December 2023
required `write_api`; those older scope requirements may still be around
on other openstreetmap-website-based servers such as
[OpenHistoricalMap](https://www.openhistoricalmap.org).

## See also

Other functions for moderators:
[`osm_create_user_block()`](https://docs.ropensci.org/osmapiR/reference/osm_create_user_block.md),
[`osm_delete_note()`](https://docs.ropensci.org/osmapiR/reference/osm_delete_note.md),
[`osm_hide_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_hide_comment_changeset_discussion.md)

## Examples

``` r
if (FALSE) { # \dontrun{
## WARNING: this example will edit the OSM (testing) DB with your user!
# You will need a user with moderator role in the server to use `osm_redaction_object()`
set_osmapi_connection(server = "testing") # setting https://master.apis.dev.openstreetmap.org
x <- data.frame(type = "node", lat = 0, lon = 0, name = "Test redaction.")
obj <- osmapi_objects(x, tag_columns = "name")
changeset_id <- osm_create_changeset(
  comment = "Test object redaction",
  hashtags = "#testing;#osmapiR"
)

node_id <- osm_create_object(x = obj, changeset_id = changeset_id)
node_osm <- osm_get_objects(osm_type = "node", osm_id = node_id)
deleted_version <- osm_delete_object(x = node_osm, changeset_id = changeset_id)
redaction <- osm_redaction_object(
  osm_type = node_osm$type, osm_id = node_osm$id, version = 1, redaction_id = 1
)
unredaction <- osm_redaction_object(osm_type = node_osm$type, osm_id = node_osm$id, version = 1)
osm_close_changeset(changeset_id = changeset_id)
} # }
```
