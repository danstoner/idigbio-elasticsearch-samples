The iDigBio API and working examples are documented in the wiki:

https://www.idigbio.org/wiki/index.php/IDigBio_API


The idigbio-elasticsearch-samples project is a bit of a scratch pad or placeholder for additional examples, etc.
that may or may not get added to the official docs.

NOTE: Some of the example json query files do not work!


To execute a query using URI search interface:

curl -s -XGET https://search.idigbio.org/idigbio/records/_search?q=uuid:a5eef658-07c3-4c45-91ef-17f21f7ccff8


To execute a query using a json file such as county.json:

$  curl -s -XGET 'https://search.idigbio.org/idigbio/records/_search' -d@county.json  | json_pp | egrep "\"county\""
               "county" : "hocking",
               "county" : "hocking",
               "county" : "hocking",
               "county" : "hocking",
               "county" : "hocking",
               "county" : "hocking",
               "county" : "hocking",
               "county" : "hocking",
               "county" : "hocking",
               "county" : "hocking",


NOTE: If the file designated by the @ sign does not exist the curl will proceed anyway and a default query against
the search URL will run (with no query parameters).

$ curl -s -XGET 'https://search.idigbio.org/idigbio/records/_search' -d@doesnotexist.json  | json_pp | egrep "\"county\""
               "county" : "palo pinto",
               "county" : "elk",
               "county" : "osage",
               "county" : "greenwood",
               "county" : "pittsburg",
               "county" : "chase",
               "county" : "jack",
               "county" : "cacadu district",
               "county" : "douglas",

