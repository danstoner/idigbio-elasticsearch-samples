## Intro

The iDigBio API and working examples are documented in the wiki:

https://www.idigbio.org/wiki/index.php/IDigBio_API

In addition to the API, an Elasticsearch interface is provided for advanced users.

This idigbio-elasticsearch-samples project is a bit of a scratch pad or placeholder for additional examples, etc.
that may or may not get added to the official docs.

*NOTE:* Some of the example json query files do not work!

## Examples

- Three ways to fetch a specific record based on iDigBio UUID.

1. Using the API (not Elasticsearch):

```
$ curl -s -XGET https://api.idigbio.org/v1/records/0cec43d8-9ad5-478a-bea1-397ab5cc4430

```

2. Using the Elasticsearch URL interface with query parameter:

```
$ curl -s -XGET https://search.idigbio.org/idigbio/records/_search?q=uuid:0cec43d8-9ad5-478a-bea1-397ab5cc4430
```

3. Using the Elasticsearch with json-formatted filter query in the message body:

```
$ cat uuid.json
{
    "filter" : {
    "term"  :  { "uuid" : "0cec43d8-9ad5-478a-bea1-397ab5cc4430" }
    }
}
$ curl -s -XGET https://search.idigbio.org/idigbio/records/_search -d@uuid.json
```


- To execute a query using a json file such as county.json:

```
$ curl -s -XGET 'https://search.idigbio.org/idigbio/records/_search' -d@county.json  | json_pp | egrep "\"county\""
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
```

*NOTE:* If the file designated by the @ sign does not exist the curl will proceed anyway and a default query against
the search URL will run (with no query parameters).

```
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

```