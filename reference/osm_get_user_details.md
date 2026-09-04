# Details of users

Details of users

## Usage

``` r
osm_get_user_details(user_id, format = c("R", "xml", "json"))
```

## Arguments

- user_id:

  The ids of the users to retrieve the details for, represented by a
  numeric or a character value (not the display names).

- format:

  Format of the output. Can be `"R"` (default), `"xml"`, or `"json"`.

## Value

For users not found, the result is empty. If `format = "R"`, returns a
data frame with one user per row.

### `format = "xml"`

Returns a
[xml2::xml_document](http://xml2.r-lib.org/reference/oldclass.md) with
the following format:

    <osm version="0.6" generator="OpenStreetMap server">
      <user id="12023" display_name="jbpbis" account_created="2007-08-16T01:35:56Z">
        <description></description>
        <company>bitbetter GmbH</company>
        <social-links>
          <link platform="mastodon">https://mastodon.social/@jbpbis</link>
        </social-links>
        <contributor-terms agreed="false"/>
        <img href="http://www.gravatar.com/avatar/somehash"/>
        <roles>
        </roles>
        <changesets count="1"/>
        <traces count="0"/>
        <blocks>
          <received count="0" active="0"/>
        </blocks>
      </user>
      <user id="210447" display_name="siebh" account_created="2009-12-20T10:11:42Z">
        <description></description>
        <contributor-terms agreed="true"/>
        <roles>
        </roles>
        <changesets count="267"/>
        <traces count="1"/>
        <blocks>
          <received count="0" active="0"/>
        </blocks>
      </user>
    </osm>

### `format = "json"`

Returns a list with the following json structure:

    {
      "version": "0.6",
      "generator": "OpenStreetMap server",
      "users": [
        {
          "user": {
            "id": 12023,
            "display_name": "jbpbis",
            "account_created": "2007-08-16T01:35:56Z",
            "description": "",
            "company": "MyCompany Ltd.",
            "social_links": [
              {
                "url": "https://mastodon.social/@jbpbis",
                "platform": "mastodon"
              }
            ],
            "contributor_terms": {
              "agreed": False
            },
            "img": {
              "href": "https://www.gravatar.com/avatar/somehash"
            },
            "roles": [],
            "changesets": {
              "count": 1
            },
            "traces": {
              "count": 0
            },
            "blocks": {
              "received": {
                "count": 0,
                "active": 0
              }
            }
          }
        },
        {
          "user": {
            "id": 210447,
            "display_name": "siebh",
            "account_created": "2009-12-20T10:11:42Z",
            "description": "",
            "contributor_terms": {
              "agreed": True
            },
            "roles": [],
            "changesets": {
              "count": 363
            },
            "traces": {
              "count": 1
            },
            "blocks": {
              "received": {
                "count": 0,
                "active": 0
              }
            }
          }
        }
      ]
    }

For single user calls, the `users` level gets dropped.

## See also

Other users' functions:
[`osm_details_logged_user()`](https://docs.ropensci.org/osmapiR/reference/osm_details_logged_user.md),
[`osm_get_preferences_user()`](https://docs.ropensci.org/osmapiR/reference/osm_preferences_user.md)

## Examples

``` r
usrs <- osm_get_user_details(user_id = c(1, 24, 44, 45, 46, 48, 49, 50))
usrs
#>   id        display_name     account_created
#> 1  1               Steve 2005-09-13 15:32:57
#> 2 24 Petter Reinholdtsen 2005-09-12 16:54:12
#> 3 44             user_44 2005-03-20 19:55:17
#> 4 45             user_45 2005-03-20 20:09:58
#> 5 46              FrankM 2005-09-08 15:11:47
#> 6 48             user_48 2005-03-21 13:43:58
#> 7 49             user_49 2005-03-21 14:58:06
#> 8 50             HeinerS 2005-03-21 15:53:06
#>                                                                                                                                                                                                                              description
#> 1                                                                                                                                                                                                                                       
#> 2                                                                                                                                                                                                                                       
#> 3                                                                                                                                                                                                                                       
#> 4                                                                                                                                                                                                                                       
#> 5 My Tracks:\n\ntr.&lt;date&gt;.edit.gpx  - Garmin Geko 301\ntr-vista.&lt;date&gt;.edit.gpx  - Garmin Vista HCx\ngps-&lt;date&gt;.gpsd.gpx - Navilock NL-303P (SIRF III)\nmm-&lt;date&gt;-mtk.gpx   - maemo mapper + BT-Q1000 (MTK Chip)
#> 6                                                                                                                                                                                                                                       
#> 7                                                                                                                                                                                                                                       
#> 8                                                                                                                                                                                                                                       
#>    img contributor_terms roles changesets_count traces_count
#> 1 <NA>              TRUE  <NA>             1183           23
#> 2 <NA>              TRUE  <NA>              568           64
#> 3 <NA>             FALSE  <NA>                0            0
#> 4 <NA>             FALSE  <NA>                0            0
#> 5 <NA>              TRUE  <NA>              825          426
#> 6 <NA>             FALSE  <NA>                0            0
#> 7 <NA>             FALSE  <NA>                0            0
#> 8 <NA>              TRUE  <NA>              140            0
#>   blocks_received.count blocks_received.active blocks_issued.count
#> 1                     0                      0                  NA
#> 2                     0                      0                  NA
#> 3                     0                      0                  NA
#> 4                     0                      0                  NA
#> 5                     0                      0                  NA
#> 6                     0                      0                  NA
#> 7                     0                      0                  NA
#> 8                     0                      0                  NA
#>   blocks_issued.active
#> 1                   NA
#> 2                   NA
#> 3                   NA
#> 4                   NA
#> 5                   NA
#> 6                   NA
#> 7                   NA
#> 8                   NA
```
