# Details of the logged-in user

You can get the home location, the display name of the user and other
details.

## Usage

``` r
osm_details_logged_user(format = c("R", "xml", "json"))
```

## Arguments

- format:

  Format of the output. Can be `"R"` (default), `"xml"`, or `"json"`.

## Value

If `format = "R"`, returns a list with the user details.

### `format = "xml"`

Returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) with
the following format:

    <osm version="0.6" generator="OpenStreetMap server">
      <user display_name="Max Muster" account_created="2006-07-21T19:28:26Z" id="1234">
        <contributor-terms agreed="true" pd="true"/>
        <img href="https://www.openstreetmap.org/attachments/users/images/000/000/1234/original/someLongURLOrOther.JPG"/>
        <roles></roles>
        <changesets count="4182"/>
        <traces count="513"/>
        <blocks>
          <received count="0" active="0"/>
        </blocks>
        <home lat="49.4733718952806" lon="8.89285988577866" zoom="3"/>
        <description>The description of your profile</description>
        <languages>
          <lang>de-DE</lang>
          <lang>de</lang>
          <lang>en-US</lang>
          <lang>en</lang>
        </languages>
        <messages>
          <received count="1" unread="0"/>
          <sent count="0"/>
        </messages>
      </user>
    </osm>

### `format = "json"`

    {
      "version": "0.6",
      "generator": "OpenStreetMap server",
      "user": {
        "id": 1234,
        "display_name": "Max Muster",
        "account_created": "2006-07-21T19:28:26Z",
        "description": "The description of your profile",
        "contributor_terms": {"agreed": True, "pd": True},
        "img": {"href": "https://www.openstreetmap.org/attachments/users/images/000/000/1234/original/someLongURLOrOther.JPG"},
        "roles": [],
        "changesets": {"count": 4182},
        "traces": {"count": 513},
        "blocks": {"received": {"count": 0, "active": 0}},
        "home": {"lat": 49.4733718952806, "lon": 8.89285988577866, "zoom": 3},
        "languages": ["de-DE", "de", "en-US", "en"],
        "messages": {"received": {"count": 1, "unread": 0},
        "sent": {"count": 0}}
      }
    }

## See also

Other users' functions:
[`osm_get_preferences_user()`](https://docs.ropensci.org/osmapiR/reference/osm_preferences_user.md),
[`osm_get_user_details()`](https://docs.ropensci.org/osmapiR/reference/osm_get_user_details.md)

## Examples

``` r
if (FALSE) { # \dontrun{
usr_details <- osm_details_logged_user()
usr_details
} # }
```
