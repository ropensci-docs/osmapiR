# Read user block

Read user block

## Usage

``` r
osm_get_user_blocks(user_block_id, format = c("R", "xml", "json"))
```

## Arguments

- user_block_id:

  The id of the user block to retrieve represented by a numeric or a
  character value.

- format:

  Format of the output. Can be `"R"` (default), `"xml"`, or `"json"`.

## Value

If `format = "R"`, returns a data frame with one row with the details of
the block.

### `format = "xml"`

Returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) with
the following format:

    <?xml version="1.0" encoding="UTF-8"?>
    <osm version="0.6" generator="OpenStreetMap server" copyright="OpenStreetMap and contributors" attribution="http://www.openstreetmap.org/copyright" license="http://opendatacommons.org/licenses/odbl/1-0/">
      <user_block id="101" created_at="2025-02-22T02:11:55Z" updated_at="2025-02-22T02:11:55Z" ends_at="2025-02-22T03:11:55Z" needs_view="true">
        <user uid="5" user="fakemod1"/>
        <creator uid="115" user="fakemod2"/>
      </user_block>
      <user_block id="100" created_at="2025-02-22T02:11:10Z" updated_at="2025-02-22T02:11:10Z" ends_at="2025-02-22T02:11:10Z" needs_view="true">
        <user uid="5" user="fakemod1"/>
        <creator uid="115" user="fakemod2"/>
      </user_block>
      ...
    </osm>

### `format = "json"`

Returns a list with the following json structure:

    {
      "version":"0.6",
      "generator":"OpenStreetMap server",
      "copyright":"OpenStreetMap and contributors",
      "attribution":"http://www.openstreetmap.org/copyright",
      "license":"http://opendatacommons.org/licenses/odbl/1-0/",
      "user_blocks":[
        {
          "id":101,
          "created_at":"2025-02-22T02:11:55Z",
          "updated_at":"2025-02-22T02:11:55Z",
          "ends_at":"2025-02-22T03:11:55Z",
          "needs_view":true,
          "user":{"uid":5,"user":"fakemod1"},
          "creator":{"uid":115,"user":"fakemod2"},
          "revoker":{"uid":115,"user":"fakemod2"},
          "reason":"reason text\r\n\r\nmore reason text"
        },
        {
          "id":100,
          "created_at":"2025-02-22T02:11:10Z",
          "updated_at":"2025-02-22T02:11:10Z",
          "ends_at":"2025-02-22T02:11:10Z",
          "needs_view":true,
          "user":{"uid":5,"user":"fakemod1"},
          "creator":{"uid":115,"user":"fakemod2"},
          "revoker":{"uid":115,"user":"fakemod2"},
          "reason":"reason text\r\n\r\nmore reason text"
        },
        ...
      ]
    }

## See also

Other user blocks' functions:
[`osm_create_user_block()`](https://docs.ropensci.org/osmapiR/reference/osm_create_user_block.md),
[`osm_list_active_user_blocks()`](https://docs.ropensci.org/osmapiR/reference/osm_list_active_user_blocks.md)

## Examples

``` r
osm_get_user_blocks(1:2)
#>   id          created_at          updated_at             ends_at needs_view
#> 1  1 2009-10-12 19:51:21 2009-10-12 19:51:58 2009-10-12 19:51:21      FALSE
#> 2  2 2009-11-12 13:57:18 2009-11-12 14:34:27 2009-11-13 01:57:18      FALSE
#>   user_uid      user creator_uid    creator revoker_uid revoker
#> 1     3560 Firefishy         735 blackadder        <NA>    <NA>
#> 2    36809    RumZum        5164   woodpeck        <NA>    <NA>
#>                                                                                                                                                                                                                                                                                                                                                                                                                                                                  reason
#> 1                                                                                                                                                                                                                                                                                                                                                                                             This is testing the soft ban feature. Firefishy is not really a bad chap.
#> 2 Dear pfoten-weg,\n\n   you have uploaded tens of thousands of objects to OSM without changing them. We believe that this must be a software malfunction on your side. Would you please explain to us what software you are using, so that we may help you to avoid such unnecessary uploads in the future. These uploads clutter the history and confuse other mappers - especially if you create changesets that span the whole planet!\n\nThank you,\nFrederik Ramm
```
