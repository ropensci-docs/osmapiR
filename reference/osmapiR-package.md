# osmapiR: 'OpenStreetMap' API

Interface to 'OpenStreetMap API' for fetching and saving data from/to
the 'OpenStreetMap' database
(<https://wiki.openstreetmap.org/wiki/API_v0.6>).

## Details

An R interface to [OpenStreetMap API
v0.6](https://wiki.openstreetmap.org/wiki/API_v0.6) for fetching and
saving raw geodata from/to the OpenStreetMap database. This package
allows to access OSM maps data as well as map notes, GPS traces,
changelogs and users data. To access the OSM map data for purposes other
than editing or exploring the history of the objects see [Related
packages](https://github.com/ropensci/osmapiR/blob/main/README.md#related-packages).

You are responsible for following the [API Usage
Policy](https://operations.osmfoundation.org/policies/api/). You can
modify the user agent of the requests by setting the option
`osmapir.user_agent`:

    options(osmapir.user_agent = "my new user agent")

Respect and follow the [standards and
conventions](https://wiki.openstreetmap.org/wiki/Editing_Standards_and_Conventions)
of the OpenStreetMap community. If you plan to do automated edits, check
the [Automated Edits code of
conduct](https://wiki.openstreetmap.org/wiki/Automated_Edits_code_of_conduct).

## Overview of the functions

All function starting with `osm_*` include calls to the server.

### OSM objects

#### Get OSM objects

[`osm_bbox_objects()`](https://docs.ropensci.org/osmapiR/reference/osm_bbox_objects.md)
Retrieve map data by bounding box

[`osm_get_objects()`](https://docs.ropensci.org/osmapiR/reference/osm_get_objects.md)
Get OSM objects

[`osm_history_object()`](https://docs.ropensci.org/osmapiR/reference/osm_history_object.md)
Get the history of an object

[`osm_relations_object()`](https://docs.ropensci.org/osmapiR/reference/osm_relations_object.md)
Relations of an object

[`osm_ways_node()`](https://docs.ropensci.org/osmapiR/reference/osm_ways_node.md)
Ways of a node

[`osmapi_objects()`](https://docs.ropensci.org/osmapiR/reference/osmapi_objects.md)
osmapi_objects

#### Edit OSM objects

[`osm_create_object()`](https://docs.ropensci.org/osmapiR/reference/osm_create_object.md)
Create an OSM object

[`osm_delete_object()`](https://docs.ropensci.org/osmapiR/reference/osm_delete_object.md)
Delete an OSM object

[`osm_update_object()`](https://docs.ropensci.org/osmapiR/reference/osm_update_object.md)
Update an OSM object

### Changesets

Every modification of the standard OSM elements has to reference an open
changeset. A changeset may contain tags just like the other elements. A
recommended tag for changesets is the key ”comment=\*” with a short
human readable description of the changes being made in that changeset.
A new changeset can be opened at any time and a changeset may be
referenced from multiple API calls. Because of this it can be closed
manually as the server can't know when one changeset ends and another
should begin. To avoid stale open changesets a mechanism is implemented
to automatically close changesets. See [OSM
wiki](https://wiki.openstreetmap.org/wiki/Changeset) for details.

#### Get changesets

[`osm_download_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_download_changeset.md)
Download a changeset in OsmChange format

[`osm_get_changesets()`](https://docs.ropensci.org/osmapiR/reference/osm_get_changesets.md)
Get changesets

[`osm_query_changesets()`](https://docs.ropensci.org/osmapiR/reference/osm_query_changesets.md)
Query changesets

#### Edit changeset

[`osm_create_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_create_changeset.md)
[`osm_update_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_create_changeset.md)
[`osm_close_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_create_changeset.md)
Create, update, or close a changeset

[`osm_diff_upload_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_diff_upload_changeset.md)
Diff (OsmChange format) upload to a changeset

#### Changeset's discussion"

[`osm_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_comment_changeset_discussion.md)
Comment a changeset

[`osm_search_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_search_comment_changeset_discussion.md)
Search comments from changeset disussions

[`osm_hide_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_hide_comment_changeset_discussion.md)
[`osm_unhide_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_hide_comment_changeset_discussion.md)
Hide or unhide a changeset comment

[`osm_subscribe_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_subscribe_changeset_discussion.md)
[`osm_unsubscribe_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_subscribe_changeset_discussion.md)
Subscribe or unsubscribe to a changeset discussion

### Map notes

This functions provides access to the
[notes](https://wiki.openstreetmap.org/wiki/Notes) feature, which allows
users to add geo-referenced textual \\post-it\\ notes.

#### Get map notes

[`osm_feed_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_feed_notes.md)
RSS Feed of notes in a bbox

[`osm_get_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_get_notes.md)
Get notes

[`osm_read_bbox_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_read_bbox_notes.md)
Retrieve notes by bounding box

[`osm_search_notes()`](https://docs.ropensci.org/osmapiR/reference/osm_search_notes.md)
Search for notes

#### Subscription to map notes

[`osm_subscribe_note()`](https://docs.ropensci.org/osmapiR/reference/osm_subscribe_note.md)
Manage subscription to notes

#### Edit map notes

osm_close_note()\]
[`osm_reopen_note()`](https://docs.ropensci.org/osmapiR/reference/osm_close_note.md)
Close or reopen a note

[`osm_create_comment_note()`](https://docs.ropensci.org/osmapiR/reference/osm_create_comment_note.md)
Create a new comment in a note

[`osm_create_note()`](https://docs.ropensci.org/osmapiR/reference/osm_create_note.md)
Create a new note

[`osm_delete_note()`](https://docs.ropensci.org/osmapiR/reference/osm_delete_note.md)
Delete a note

### GPS' traces

In violation of the [GPX
standard](https://www.topografix.com/GPX/1/1/#type_trksegType) when
downloading public GPX traces through the API, all waypoints of
non-trackable traces are randomized (or rather sorted by lat/lon) and
delivered as one trackSegment for privacy reasons. Trackable traces are
delivered, sorted by descending upload time, before the waypoints of
non-trackable traces.

#### Get GPS traces

[`osm_get_data_gpx()`](https://docs.ropensci.org/osmapiR/reference/osm_get_data_gpx.md)
Download GPS Track Data

[`osm_get_gpx_metadata()`](https://docs.ropensci.org/osmapiR/reference/osm_get_gpx_metadata.md)
Download GPS Track Metadata

[`osm_get_points_gps()`](https://docs.ropensci.org/osmapiR/reference/osm_get_points_gps.md)
Get GPS Points

[`osm_list_gpxs()`](https://docs.ropensci.org/osmapiR/reference/osm_list_gpxs.md)
List user's GPX traces

#### Edit GPS traces

[`osm_create_gpx()`](https://docs.ropensci.org/osmapiR/reference/osm_create_gpx.md)
Create GPS trace

[`osm_delete_gpx()`](https://docs.ropensci.org/osmapiR/reference/osm_delete_gpx.md)
Delete GPS trace

[`osm_update_gpx()`](https://docs.ropensci.org/osmapiR/reference/osm_update_gpx.md)
Update GPS trace

### Users

[`osm_details_logged_user()`](https://docs.ropensci.org/osmapiR/reference/osm_details_logged_user.md)
Details of the logged-in user

[`osm_get_preferences_user()`](https://docs.ropensci.org/osmapiR/reference/osm_preferences_user.md)
[`osm_set_preferences_user()`](https://docs.ropensci.org/osmapiR/reference/osm_preferences_user.md)
Get or set preferences of the logged-in user

[`osm_get_user_details()`](https://docs.ropensci.org/osmapiR/reference/osm_get_user_details.md)
Details of users

### OsmChange

The [OsmChange](https://wiki.openstreetmap.org/wiki/OsmChange) format
can be uploaded to the server. This is guaranteed to be running in a
transaction. So either all the changes are applied or none. To avoid
performance issues when uploading multiple objects, the use of the
[`osm_diff_upload_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_diff_upload_changeset.md)
is highly recommended.

[`osm_diff_upload_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_diff_upload_changeset.md)
Diff (OsmChange format) upload to a changeset

[`osm_download_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_download_changeset.md)
Download a changeset in OsmChange format

[`osmchange_create()`](https://docs.ropensci.org/osmapiR/reference/osmchange_create.md)
osmchange to create OSM objects

[`osmchange_delete()`](https://docs.ropensci.org/osmapiR/reference/osmchange_delete.md)
osmchange to delete existing OSM objects

[`osmchange_modify()`](https://docs.ropensci.org/osmapiR/reference/osmchange_modify.md)
osmchange to modify existing OSM objects

### User blocks

[`osm_create_user_block()`](https://docs.ropensci.org/osmapiR/reference/osm_create_user_block.md)
Create a user block

[`osm_get_user_blocks()`](https://docs.ropensci.org/osmapiR/reference/osm_get_user_blocks.md)
Details of user blocks

[`osm_list_active_user_blocks()`](https://docs.ropensci.org/osmapiR/reference/osm_list_active_user_blocks.md)
List active blocks of the logged user

### Methods

[`tags_list2wide()`](https://docs.ropensci.org/osmapiR/reference/tags_list-wide.md)
[`tags_wide2list()`](https://docs.ropensci.org/osmapiR/reference/tags_list-wide.md)
Change tags from a list column \<-\> columns for each key in wide format

[`st_as_sf()`](https://docs.ropensci.org/osmapiR/reference/st_as_sf.md)
Convert osmapiR objects to sf objects

### API

[`set_osmapi_connection()`](https://docs.ropensci.org/osmapiR/reference/API_configuration.md)
[`get_osmapi_url()`](https://docs.ropensci.org/osmapiR/reference/API_configuration.md)
[`set_osmapi_url()`](https://docs.ropensci.org/osmapiR/reference/API_configuration.md)
Configure connections from osmapiR

[`authenticate_osmapi()`](https://docs.ropensci.org/osmapiR/reference/authenticate_osmapiR.md)
[`logout_osmapi()`](https://docs.ropensci.org/osmapiR/reference/authenticate_osmapiR.md)
Authenticate or logout osmapiR

[`osm_api_versions()`](https://docs.ropensci.org/osmapiR/reference/osm_api_versions.md)
Available API versions

[`osm_capabilities()`](https://docs.ropensci.org/osmapiR/reference/osm_capabilities.md)
Capabilities of the API

[`osm_permissions()`](https://docs.ropensci.org/osmapiR/reference/osm_permissions.md)
Retrieving permissions

### For moderators

[`osm_delete_note()`](https://docs.ropensci.org/osmapiR/reference/osm_delete_note.md)
Delete a note

[`osm_hide_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_hide_comment_changeset_discussion.md)
[`osm_unhide_comment_changeset_discussion()`](https://docs.ropensci.org/osmapiR/reference/osm_hide_comment_changeset_discussion.md)
Hide or unhide a changeset comment

[`osm_redaction_object()`](https://docs.ropensci.org/osmapiR/reference/osm_redaction_object.md)
Redact an object version

## See also

Useful links:

- <https://docs.ropensci.org/osmapiR/>

- <https://github.com/ropensci/osmapiR>

- Report bugs at <https://github.com/ropensci/osmapiR/issues>

## Author

**Maintainer**: Joan Maspons <joanmaspons@gmail.com>
([ORCID](https://orcid.org/0000-0003-2286-8727)) \[copyright holder\]

Authors:

- Joan Maspons <joanmaspons@gmail.com>
  ([ORCID](https://orcid.org/0000-0003-2286-8727)) \[copyright holder\]

Other contributors:

- Jon Harmon ([ORCID](https://orcid.org/0000-0003-4781-4346)) (Jon
  reviewed the package for rOpenSci, see
  https://github.com/ropensci/software-review/issues/633) \[reviewer\]

- Carlos Cámara ([ORCID](https://orcid.org/0000-0002-9378-0549)) (Carles
  reviewed the package for rOpenSci, see
  https://github.com/ropensci/software-review/issues/633) \[reviewer\]
