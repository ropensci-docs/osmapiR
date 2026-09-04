# Get or set preferences for the logged-in user

Get or set preferences for the logged-in user

## Usage

``` r
osm_get_preferences_user(key, format = c("R", "xml", "json"))

osm_set_preferences_user(key, value, all_prefs)
```

## Arguments

- key:

  Returns a string with this preference's value. If missing, return all
  preferences.

- format:

  Format of the output. Can be `"R"` (default), `"xml"`, or `"json"`.
  Only relevant when `key` is missing.

- value:

  A string with the preference value to set for `key`. If `NULL`,
  deletes the `key` preference.

- all_prefs:

  A `data.frame`, `xml_document` or a json list following the format
  returned by `osm_get_preferences_user()`. Also, a path to an xml file
  describing the user preferences. **All** existing preferences are
  replaced by the newly uploaded set.

## Value

If `format = "R"`, returns a data frame with `key` and `value` columns
of the user preferences.

### `format = "xml"`

Returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) with
the following format:

    <osm version="0.6" generator="OpenStreetMap server">
      <preferences>
        <preference k="somekey" v="somevalue" />
        ...
      </preferences>
    </osm>

### `format = "json"`

Returns a list with the following json structure:

    {
      "version": "0.6",
      "generator": "OpenStreetMap server",
      "preferences": {"somekey": "somevalue, ...}
    }

### Set preferences

Nothing is returned upon successful setting of user preferences.

## Details

The sizes of the key and value are limited to 255 characters.

The OSM server supports storing arbitrary user preferences. This can be
used by editors, for example, to offer the same configuration wherever
the user logs in, instead of a locally-stored configuration. For an
overview of applications using the preferences-API and which key-schemes
they use, see [this wiki
page](https://wiki.openstreetmap.org/wiki/Preferences).

## See also

Other users' functions:
[`osm_details_logged_user()`](https://docs.ropensci.org/osmapiR/reference/osm_details_logged_user.md),
[`osm_get_user_details()`](https://docs.ropensci.org/osmapiR/reference/osm_get_user_details.md)

## Examples

``` r
if (FALSE) { # \dontrun{
prefs_ori <- osm_get_preferences_user()
prefs_ori


osm_set_preferences_user(key = "osmapiR-test", value = "good!")
osm_get_preferences_user(key = "osmapiR-test")

osm_set_preferences_user(key = "osmapiR-test", value = NULL) # Delete pref

## Restore all preferences
osm_set_preferences_user(all_prefs = prefs_ori)
} # }
```
