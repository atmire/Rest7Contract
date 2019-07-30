# Bundles Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**/api/core/bundles**   

The main endpoint is not used

## Single Bundle
**/api/core/bundles/<:uuid>**

Provide detailed information about a specific bundle. A sample JSON response document is included below
```json
{
  "uuid": "d3599177-0408-403b-9f8d-d300edd79edb",
  "name": "ORIGINAL",
  "handle": null,
  "metadata": {},
  "type": "bundle",
  "_links" : {
    "primarybitstream" : {
      "href" : "https://dspace7-entities.atmire.com/rest/api/core/bitstreams/ac49f361-4ffd-47a4-8eb2-e6c73c3f3e76"
    },
    "orderedbitstreams" : {
      "href" : "https://dspace7-entities.atmire.com/rest/api/core/bundle/d3599177-0408-403b-9f8d-d300edd79edb/bitstreams"
    },
    "self" : {
      "href" : "https://dspace7-entities.atmire.com/rest/api/core/bundle/d3599177-0408-403b-9f8d-d300edd79edb"
    }
  },
   "_embedded" : {
      "orderedbitstreams" : [ {
        "id" : "1ce6db0e-662f-4a13-ba87-c371ad664b14",
        "uuid" : "1ce6db0e-662f-4a13-ba87-c371ad664b14",
        "name" : "atmire-logo.jpeg",
        "handle" : null,
        "metadata" : {
          "dc.description" : [ {
            "value" : "",
            "language" : null,
            "authority" : null,
            "confidence" : -1,
            "place" : 0
          } ],
          "dc.source" : [ {
            "value" : "atmire-logo.jpeg",
            "language" : null,
            "authority" : null,
            "confidence" : -1,
            "place" : 0
          } ],
          "dc.title" : [ {
            "value" : "atmire-logo.jpeg",
            "language" : null,
            "authority" : null,
            "confidence" : -1,
            "place" : 0
          } ]
        },
        "bundleName" : "ORIGINAL",
        "sizeBytes" : 7568,
        "checkSum" : {
          "checkSumAlgorithm" : "MD5",
          "value" : "59a4cfd819ce67ba7252efc52d1eb99b"
        },
        "sequenceId" : null,
        "type" : "bitstream",
        "_links" : {
          "content" : {
            "href" : "http://10.211.55.20:8080/server/api/core/bitstreams/1ce6db0e-662f-4a13-ba87-c371ad664b14/content"
          },
          "format" : {
            "href" : "http://10.211.55.20:8080/server/api/core/bitstreams/1ce6db0e-662f-4a13-ba87-c371ad664b14/format"
          },
          "self" : {
            "href" : "http://10.211.55.20:8080/server/api/core/bitstreams/1ce6db0e-662f-4a13-ba87-c371ad664b14"
          }
        }
      }, {
        "id" : "4dd9621f-a464-4192-bc17-d70f68845bdc",
        "uuid" : "4dd9621f-a464-4192-bc17-d70f68845bdc",
        "name" : "atmire-logo.jpeg.jpg",
        "handle" : null,
        "metadata" : {
          "dc.description" : [ {
            "value" : "Generated Thumbnail",
            "language" : null,
            "authority" : null,
            "confidence" : -1,
            "place" : 0
          } ],
          "dc.source" : [ {
            "value" : "Written by FormatFilter org.dspace.app.mediafilter.JPEGFilter on 2018-05-30T14:28:19Z (GMT).",
            "language" : null,
            "authority" : null,
            "confidence" : -1,
            "place" : 0
          } ],
          "dc.title" : [ {
            "value" : "atmire-logo.jpeg.jpg",
            "language" : null,
            "authority" : null,
            "confidence" : -1,
            "place" : 0
          } ]
        },
        "bundleName" : "THUMBNAIL",
        "sizeBytes" : 4825,
        "checkSum" : {
          "checkSumAlgorithm" : "MD5",
          "value" : "78647c1fab73a7aa7c97fdfc538ee6d4"
        },
        "sequenceId" : null,
        "type" : "bitstream",
        "_links" : {
          "content" : {
            "href" : "http://10.211.55.20:8080/server/api/core/bitstreams/4dd9621f-a464-4192-bc17-d70f68845bdc/content"
          },
          "format" : {
            "href" : "http://10.211.55.20:8080/server/api/core/bitstreams/4dd9621f-a464-4192-bc17-d70f68845bdc/format"
          },
          "self" : {
            "href" : "http://10.211.55.20:8080/server/api/core/bitstreams/4dd9621f-a464-4192-bc17-d70f68845bdc"
          }
        }
      }
    ]
  }
}
```

Exposed links:
* primarybitstream: link to the primary bitstream if present, it will be embedded
* orderedbitstreams: link to the list of bitstreams displayed according to the order specified by the bundle, it will be embedded

## Ordering bitstreams

**PATCH /api/core/bundles/<:uuid>**

Bitstreams may be re-ordered with the PATCH `move` operation.

Current list of bitstreams:
```json
{
  "orderedbitstreams" : [ 
      {
        "id" : "1ce6db0e-662f-4a13-ba87-c371ad664b14",
        "uuid" : "1ce6db0e-662f-4a13-ba87-c371ad664b14",
        "_links" : {
          "self" : {
            "href" : "http://10.211.55.20:8080/server/api/core/bitstreams/1ce6db0e-662f-4a13-ba87-c371ad664b14"
          }
        }
      }, {
        "id" : "4dd9621f-a464-4192-bc17-d70f68845bdc",
        "uuid" : "4dd9621f-a464-4192-bc17-d70f68845bdc",
        "_links" : {
          "self" : {
            "href" : "http://10.211.55.20:8080/server/api/core/bitstreams/4dd9621f-a464-4192-bc17-d70f68845bdc"
          }
        }
      }
  ]
}
```

Example request, moving the last bitstream to the first position:

```json
[
  {
    "op": "move",
    "from": "/_links/orderedbitstreams/1/href",
    "path": "/_links/orderedbitstreams/0/href"
  }
]
```

New list of bitstreams:

```json
{
  "orderedbitstreams" : [ 
      {
        "id" : "4dd9621f-a464-4192-bc17-d70f68845bdc",
        "uuid" : "4dd9621f-a464-4192-bc17-d70f68845bdc",
        "_links" : {
          "self" : {
            "href" : "http://10.211.55.20:8080/server/api/core/bitstreams/4dd9621f-a464-4192-bc17-d70f68845bdc"
          }
        }
      },
      {
        "id" : "1ce6db0e-662f-4a13-ba87-c371ad664b14",
        "uuid" : "1ce6db0e-662f-4a13-ba87-c371ad664b14",
        "_links" : {
          "self" : {
            "href" : "http://10.211.55.20:8080/server/api/core/bitstreams/1ce6db0e-662f-4a13-ba87-c371ad664b14"
          }
        }
      }
  ]
}
```
