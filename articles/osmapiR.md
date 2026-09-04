# osmapiR

osmapiR can fetch and edit all kinds data associated with the
[OpenStreetMap](https://www.openstreetmap.org) project. This vignette
shows samples of each data type and how to configure the connection to
the servers.

Most of the functions have a `format` argument that allows to modify the
result to get the raw xml or a JSON list. By default, the results are
data.frames. Check the documentation of each function for details.

## Setup

``` r

library(osmapiR)
#> Data (c) OpenStreetMap contributors, ODbL 1.0. https://www.openstreetmap.org/copyright
```

For testing editions without breaking the OSM data, you can open and
account and make calls to <https://master.apis.dev.openstreetmap.org>.

``` r

# set_osmapi_connection(server = "testing") # lacks data for the following examples
```

To modify the default user agent of the requests
(`osmapiR 0.2.6.9000 (https://github.com/ropensci/osmapiR)`), set the
option `osmapir.user_agent`:

``` r

options(osmapir.user_agent = "my new user agent")
```

## Map objects

``` r

## Download objects by bounding box
osm_objs <- osm_bbox_objects(
  bbox = c(2.4166059, 42.5945594, 2.4176574, 42.5962101)
)
head(osm_objs)
#>   type        id visible version changeset           timestamp     user   uid
#> 1 node 521349679    TRUE       3  14832699 2013-01-29 10:08:52 petrovsk 90394
#> 2 node 521349680    TRUE       3  14832699 2013-01-29 10:08:52 petrovsk 90394
#> 3 node 521349681    TRUE       3  14832699 2013-01-29 10:08:52 petrovsk 90394
#> 4 node 639618608    TRUE       2 103004865 2021-04-15 15:41:02 petrovsk 90394
#> 5 node 639618609    TRUE       2 103004865 2021-04-15 15:41:02 petrovsk 90394
#> 6 node 639618610    TRUE       2 103004865 2021-04-15 15:41:02 petrovsk 90394
#>          lat       lon members    tags
#> 1 42.5961954 2.4186301    NULL No tags
#> 2 42.5966411 2.4184297    NULL No tags
#> 3 42.5973670 2.4177800    NULL No tags
#> 4 42.5945781 2.4167126    NULL No tags
#> 5 42.5948055 2.4166170    NULL No tags
#> 6 42.5948686 2.4168323    NULL No tags

# osm_objs$tags # tags in list format

## View the history of an object
sel <- sapply(osm_objs$tags, function(x) any(x$key == "name:ca" & x$value == "Abadia de Sant Miquel de Cuixà"))
obj <- osm_objs[sel, ]

obj_history <- osm_history_object(
  osm_type = obj$type[1], osm_id = obj$id[1],
  tags_in_columns = TRUE
)
obj_history
#>   osm_type   osm_id visible version changeset           timestamp       user
#> 1      way 50343004    TRUE       1   3882565 2010-02-15 12:14:11    Skywave
#> 2      way 50343004    TRUE       2  13314595 2012-09-30 19:52:28   petrovsk
#> 3      way 50343004    TRUE       3  53623614 2017-11-08 22:08:33      JFK73
#> 4      way 50343004    TRUE       4 103004865 2021-04-15 15:41:02   petrovsk
#> 5      way 50343004    TRUE       5 164200317 2025-03-28 10:16:25 X-Cyclette
#>        uid  lat  lon
#> 1    10927 <NA> <NA>
#> 2    90394 <NA> <NA>
#> 3   662440 <NA> <NA>
#> 4    90394 <NA> <NA>
#> 5 16689426 <NA> <NA>
#>                                                           members
#> 1 44 nodes: 639618609, 639618608, 639618720, 639618717, 639618...
#> 2 44 nodes: 639618609, 639618608, 639618720, 639618717, 639618...
#> 3 44 nodes: 639618609, 639618608, 639618720, 639618717, 639618...
#> 4 48 nodes: 639618609, 639618608, 8632687795, 8632687796, 8632...
#> 5 48 nodes: 639618609, 639618608, 8632687795, 8632687796, 8632...
#>            amenity building denomination heritage heritage:operator  historic
#> 1 place_of_worship      yes     catholic     <NA>              <NA> monastery
#> 2 place_of_worship      yes     catholic     <NA>              <NA> monastery
#> 3 place_of_worship      yes     catholic        2               mhs monastery
#> 4 place_of_worship      yes     catholic        2               mhs monastery
#> 5 place_of_worship      yes     catholic        2               mhs monastery
#>   mhs:inscription_date                           name
#> 1                 <NA> Abbaye de Saint Michel de Cuxa
#> 2                 <NA> Abbaye de Saint-Michel de Cuxa
#> 3           1958-04-15 Abbaye de Saint-Michel de Cuxa
#> 4           1958-04-15 Abbaye de Saint-Michel de Cuxa
#> 5           1958-04-15 Abbaye de Saint-Michel de Cuxa
#>                          name:ca
#> 1 Abadia de Sant Miquel de Cuixa
#> 2 Abadia de Sant Miquel de Cuixa
#> 3 Abadia de Sant Miquel de Cuixà
#> 4 Abadia de Sant Miquel de Cuixà
#> 5 Abadia de Sant Miquel de Cuixà
#>                                                                    note
#> 1                                                                  <NA>
#> 2                                                                  <NA>
#> 3                                                                  <NA>
#> 4                                                                  <NA>
#> 5 Photogrammétrie:\nhttps://xcyclette.site/Abbaye-Saint-Michel-de-Cuxa/
#>      ref:mhs  religion
#> 1       <NA> christian
#> 2       <NA> christian
#> 3 PA00103995 christian
#> 4 PA00103995 christian
#> 5 PA00103995 christian
#>                                                                                   source
#> 1 cadastre-dgi-fr source : Direction Générale des Impôts - Cadastre ; mise à jour : 2010
#> 2 cadastre-dgi-fr source : Direction Générale des Impôts - Cadastre ; mise à jour : 2010
#> 3 cadastre-dgi-fr source : Direction Générale des Impôts - Cadastre ; mise à jour : 2010
#> 4 cadastre-dgi-fr source : Direction Générale des Impôts - Cadastre ; mise à jour : 2010
#> 5   cadastre-dgi-fr source : Direction Générale des Impôts - Cadastre;mise à jour : 2010
#>                                  source:heritage wikidata
#> 1                                           <NA>     <NA>
#> 2                                           <NA>     <NA>
#> 3 data.gouv.fr:Ministère de la Culture - 04/2015  Q306121
#> 4 data.gouv.fr:Ministère de la Culture - 04/2015  Q306121
#> 5 data.gouv.fr:Ministère de la Culture - 04/2015  Q306121
#>                        wikipedia
#> 1                           <NA>
#> 2                           <NA>
#> 3 fr:Abbaye Saint-Michel de Cuxa
#> 4 fr:Abbaye Saint-Michel de Cuxa
#> 5 fr:Abbaye Saint-Michel de Cuxa
```

Notice the different formats to represent the tags controlled by the
`tags_in_columns` argument. In `osm_objs` there is a `tag` column
containing a list of data.frames with `key` and `value` columns (list
format), while in `obj_history` every tag is represented by a column in
the data.frame (wide format). See `?tags_list2wide()` for details.

## Changesets

``` r

chsts <- osm_query_changesets(
  bbox = c(2.65, 42.68, 2.71, 42.69),
  user = "Quercinus",
  time = "2023-06-20",
  time_2 = "2023-06-22"
)
chsts
#>          id          created_at           closed_at  open      user      uid
#> 1 137595351 2023-06-21 09:09:18 2023-06-21 09:09:18 FALSE Quercinus 19641470
#>      min_lat   min_lon    max_lat   max_lon comments_count changes_count
#> 1 42.6799619 2.6580564 42.6936802 2.7125775              4             1
#>                                                                                  tags
#> 1 8 tags: changesets_count=1 | comment=Correcció d'acord amb la toponímia oficial ...

osmchange <- osm_download_changeset(changeset_id = 137595351, format = "xml")
osmchange
#> {xml_document}
#> <osmChange version="0.6" generator="openstreetmap-cgimap 2.1.0 (1714912 spike-08.openstreetmap.org)" copyright="OpenStreetMap and contributors" attribution="http://www.openstreetmap.org/copyright" license="http://opendatacommons.org/licenses/odbl/1-0/">
#> [1] <modify>\n  <way id="32570900" visible="true" version="9" changeset="1375 ...

# Osmchange file compatible with JOSM and others:
# xml2::write_xml(osmchange, file = tempfile(fileext = ".osc"))
```

Similar to the map objects, changeset’s data also have the tags as a
list column that can be changed with `tags_in_columns` argument.

## Notes

``` r

notes <- osm_read_bbox_notes(bbox = "2.4166059,42.5945594,2.4176574,42.5962101", closed = -1)
notes
#>         lon        lat      id
#> 1 2.4170566 42.5948042 1730475
#> 2 2.4170552 42.5949259  628602
#>                                                       url comment_url close_url
#> 1 https://api.openstreetmap.org/api/0.6/notes/1730475.xml        <NA>      <NA>
#> 2  https://api.openstreetmap.org/api/0.6/notes/628602.xml        <NA>      <NA>
#>          date_created status
#> 1 2019-03-31 14:10:04 closed
#> 2 2016-07-15 07:09:19 closed
#>                                                          comments
#> 1                     2 comments from 2019-03-31 by Sherpa66, Syl
#> 2 5 comments from 2016-07-15 to 2018-05-25 by Dolfo54, rainerU...

# notes$comments
```

## GPX data

``` r

## Requires authentication
usr_traces <-  osm_list_gpxs()
osm_get_gpx_metadata(gpx_id = 3790367)
#>        id                 name      uid     user visibility pending           timestamp
#> 1 3790367 Airoto_Marimanha.gpx 11725140 jmaspons     public   FALSE 2021-08-20 10:30:15 
#>                 lat                lon               description              tags
#> 1 42.69660229794681 1.0419843904674053 Airoto Marimanha Oriental 1 camp, a, través
pts <- osm_get_data_gpx(gpx_id = 3790367, format = "R")
head(pts)
#>                  lat                lon               ele                time
#> 1  42.69660229794681 1.0419843904674053 2190.199951171875 2021-08-12 09:52:18
#> 2  42.69662777893245   1.04197240434587              2189 2021-08-12 09:52:24
#> 3  42.69664118997753  1.041965363547206  2188.39990234375 2021-08-12 09:52:25
#> 4  42.69665057770908 1.0419651120901108 2187.800048828125 2021-08-12 09:52:26
#> 5 42.696685614064336 1.0419511143118143 2186.800048828125 2021-08-12 09:52:29
#> 6  42.69673557020724 1.0419355239719152              2187 2021-08-12 09:52:34
```

``` r

gpx <- osm_get_points_gps(bbox = c(2.4166059, 42.5945594, 2.4176574, 42.5962101))
gpx
#> [[1]]
#>          lat       lon
#> 1 42.5945734 2.4166662
#> 2 42.5945770 2.4166060
#> 3 42.5945770 2.4166640
#> 4 42.5945770 2.4166880
#> 5 42.5945800 2.4166300
#> 6 42.5945890 2.4167120
#> 7 42.5945999 2.4166340
#> 8 42.5946030 2.4166390
#> 9 42.5946100 2.4166260
#> 
#> attr(,"gpx_attributes")
#>                             version                             creator 
#>                               "1.0"                 "OpenStreetMap.org" 
#>                               xmlns 
#> "http://www.topografix.com/GPX/1/0" 
#> attr(,"class")
#> [1] "osmapi_gpx" "list"
```

## Users

``` r

usrs <- osm_get_user_details(user_id = c(1, 24, 44, 45))
usrs
#>   id        display_name     account_created description  img contributor_terms
#> 1  1               Steve 2005-09-13 15:32:57             <NA>              TRUE
#> 2 24 Petter Reinholdtsen 2005-09-12 16:54:12             <NA>              TRUE
#> 3 44             user_44 2005-03-20 19:55:17             <NA>             FALSE
#> 4 45             user_45 2005-03-20 20:09:58             <NA>             FALSE
#>   roles changesets_count traces_count blocks_received.count
#> 1  <NA>             1183           23                     0
#> 2  <NA>              568           64                     0
#> 3  <NA>                0            0                     0
#> 4  <NA>                0            0                     0
#>   blocks_received.active blocks_issued.count blocks_issued.active
#> 1                      0                  NA                   NA
#> 2                      0                  NA                   NA
#> 3                      0                  NA                   NA
#> 4                      0                  NA                   NA
```
