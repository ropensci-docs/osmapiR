# Diff (OsmChange format) upload to a changeset

With this API call files in the
[OsmChange](https://wiki.openstreetmap.org/wiki/OsmChange) format can be
uploaded to the server. This is guaranteed to be running in a
transaction. So either all the changes are applied or none.

## Usage

``` r
osm_diff_upload_changeset(changeset_id, osmcha, format = c("R", "xml"))
```

## Arguments

- changeset_id:

  The ID of the changeset this diff belongs to. The user issuing this
  API call has to be the same that created the changeset.

- osmcha:

  The OsmChange data. Can be the path of an OsmChange file, a
  [xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) or
  an `osmapi_OsmChange` object (see `osmchange_*()` functions).

- format:

  Format of the output. Can be `"R"` (default) or `"xml"`.

## Value

If a diff is successfully applied and `format = "R"`, it returns a data
frame with one row for each edited object. For `format = "xml"`, a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) is
returned in the following format:

    <diffResult generator="OpenStreetMap Server" version="0.6">
      <node|way|relation old_id="#" new_id="#" new_version="#"/>
      ...
    </diffResult>

with one element for every object in the upload.

Note that this can be counter-intuitive when the same element has
appeared multiple times in the input then it will appear multiple times
in the output.

|  |  |  |  |
|----|----|----|----|
| **Attribute** | **create** | **modify** | **delete** |
| **old_id** | same as uploaded element | same as uploaded element | same as uploaded element |
| **new_id** | new ID | new ID ”or” same as uploaded | not present |
| **new_version** | new version | new version | not present |

## Details

To upload an OSC file it has to conform to the
[OsmChange](https://wiki.openstreetmap.org/wiki/OsmChange) specification
with the following differences:

- each element must carry a `changeset` and a `version` attribute (xml)
  / column (data.frame), except when you are creating an element where
  the version is not required as the server sets that for you. The
  `changeset` must be the same as the changeset ID being uploaded to.

- a `<delete>` block in the OsmChange document may have an `if-unused`
  attribute (the value of which is ignored) (`action_type` column with
  `delete if-unused` for data.frames). If this attribute is present,
  then the delete operation(s) in this block are conditional and will
  only be executed if the object to be deleted is not used by another
  object. Without the `if-unused`, such a situation would lead to an
  error, and the whole diff upload would fail. Setting the attribute
  will also cause deletions of already deleted objects to not generate
  an error.

- [OsmChange](https://wiki.openstreetmap.org/wiki/OsmChange) documents
  generally have `user` and `uid` attributes on each element. These are
  not required in the document uploaded to the API.

## Note

- Processing stops at the first error, so if there are multiple
  conflicts in one diff upload, only the first problem is reported.

- Refer to
  [`osm_capabilities()`](https://docs.ropensci.org/osmapiR/reference/osm_capabilities.md)
  –\> `changesets$maximum_elements` for the maximum number of changes
  permitted in a changeset.

- There is currently no limit in the diff size on the Rails port. CGImap
  limits diff size to 50MB (uncompressed size).

- Forward referencing of placeholder ids is not permitted and will be
  rejected by the API.

## See also

Other edit changeset's functions:
[`osm_create_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_create_changeset.md)

Other OsmChange's functions:
[`osm_download_changeset()`](https://docs.ropensci.org/osmapiR/reference/osm_download_changeset.md),
[`osmchange_create()`](https://docs.ropensci.org/osmapiR/reference/osmchange_create.md),
[`osmchange_delete()`](https://docs.ropensci.org/osmapiR/reference/osmchange_delete.md),
[`osmchange_modify()`](https://docs.ropensci.org/osmapiR/reference/osmchange_modify.md)

## Examples

``` r
vignette("how_to_edit_osm", package = "osmapiR")
#> Warning: vignette ‘how_to_edit_osm’ not found
```
