# List active blocks

Allows to check if the currently authorized user is blocked.

## Usage

``` r
osm_list_active_user_blocks(format = c("R", "xml", "json"))
```

## Arguments

- format:

  Format of the output. Can be `"R"` (default), `"xml"`, or `"json"`.

## Value

If `format = "R"`, returns a data frame with one row per block. No rows,
no blocks.

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

Empty `<osm>` element indicates no active blocks.

### `format = "json"`

Returns a list with the following json structure:

    {
      "version":"0.6","generator":"OpenStreetMap server","copyright":"OpenStreetMap and contributors","attribution":"http://www.openstreetmap.org/copyright","license":"http://opendatacommons.org/licenses/odbl/1-0/",
      "user_blocks":[
        {
          "id":101,
          "created_at":"2025-02-22T02:11:55Z",
          "updated_at":"2025-02-22T02:11:55Z",
          "ends_at":"2025-02-22T03:11:55Z",
          "needs_view":true,
          "user":{"uid":5,"user":"fakemod1"},
          "creator":{"uid":115,"user":"fakemod2"}
        },
        {
          "id":100,
          "created_at":"2025-02-22T02:11:10Z",
          "updated_at":"2025-02-22T02:11:10Z",
          "ends_at":"2025-02-22T02:11:10Z",
          "needs_view":true,
          "user":{"uid":5,"user":"fakemod1"},
          "creator":{"uid":115,"user":"fakemod2"}
        },
        ...
      ]
    }

## Details

This endpoint is accessible even with an active block, unlike some other
endpoints requiring authorization.

## See also

Other user blocks' functions:
[`osm_create_user_block()`](https://docs.ropensci.org/osmapiR/reference/osm_create_user_block.md),
[`osm_get_user_blocks()`](https://docs.ropensci.org/osmapiR/reference/osm_get_user_blocks.md)

## Examples

``` r
if (FALSE) { # \dontrun{
osm_list_active_user_blocks()
} # }
```
