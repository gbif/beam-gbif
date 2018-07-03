# Accessing content from the GBIF API

This pages describes how to issue a download. 

### TLDR
You can use [this example (236MB avro)](http://api.gbif.org/v1/occurrence/download/request/0035891-180508205500799.avro) citing as:
> GBIF.org (03 July 2018) GBIF Occurrence Download [https://doi.org/10.15468/dl.nkuzoz](https://doi.org/10.15468/dl.nkuzoz)

### Running downloads

The [GBIF occurrence API](https://www.gbif.org/developer/occurrence) has an undocumented feature to retrieve content in Avro format which is used below.

#### Prerequisites
To download, you must first [create an account](https://www.gbif.org/) on GBIF.org.

#### Running a download
You can use [the website](https://www.gbif.org/occurrence/search?license=CC0_1_0&year=2017&has_coordinate=true&taxon_key=212&has_geospatial_issue=false) to create searches and downoad, or use the API.
Only the API can do Avro format at the moment.

Create a search request and save it as a file, such as this example (birds observed in 2017 with coordinates and a CC0 waiver):
```
{
  "creator": "trobertson",
  "notification_address": [
    "trobertson@gbif.org"
  ],
  "format": "SIMPLE_AVRO",
  "predicate": {
    "type": "and",
    "predicates": [
      {
        "type": "equals",
        "key": "LICENSE",
        "value": "CC0_1_0"
      },
      {
        "type": "equals",
        "key": "YEAR",
        "value": "2017"
      },
      {
        "type": "equals",
        "key": "HAS_COORDINATE",
        "value": "true"
      },
      {
        "type": "equals",
        "key": "TAXON_KEY",
        "value": "212"
      },
      {
        "type": "equals",
        "key": "HAS_GEOSPATIAL_ISSUE",
        "value": "false"
      }
    ]
  }
}
```

Execute the request using curl (adding your username/password)
```
curl -i --user trobertson:*** -H "Content-Type: application/json" -X POST -d @query-georef-birds-2017.json 'https://api.gbif.org/v1/occurrence/download/request'
``` 

There is an API to poll the job progress, but it is easiest to wait for the email or [look at your downloads](https://www.gbif.org/user/download) on the GBIF.org site.

The above query was already executed and can be downloaded as avro [here](http://api.gbif.org/v1/occurrence/download/request/0035891-180508205500799.avro).

If used, please cite it as:
> GBIF.org (03 July 2018) GBIF Occurrence Download [https://doi.org/10.15468/dl.nkuzoz](https://doi.org/10.15468/dl.nkuzoz)

