# Metadata Fields Endpoints
[Back to the list of all defined endpoints](endpoints.md)

All the API requests below require admin permissions

**/api/core/<:type>/<:uuid>/exportToCsv**

Example: <https://dspace7-internal.atmire.com/rest/#https://dspace7-internal.atmire.com/rest/api/core/collections/8a085042-ba77-11e8-96f8-529269fb1459/exportToCsv>

It should provide access to the list of exports for this community/collection/item.

The json representation is as follow
```json
{
  "type": "exportToCsv",
  "_links": {
    "create": {
      "href": "https://dspace7-internal.atmire.com/rest/api/core/collection/exportToCsv/collections/8a085042-ba77-11e8-96f8-529269fb1459/exportToCsv/create"
    },
    "self": {
      "href": "https://dspace7-internal.atmire.com/rest/api/core/collections/8a085042-ba77-11e8-96f8-529269fb1459/exportToCsv"
    }
  },
  "_embedded": {
    "exportToCsv": [
      {
        "date": "2018-09-17T09:24:24.000+0000",
        "state": "completed",
        "size": 6427,
        "type": "collections",
        "dso-id": "8a085042-ba77-11e8-96f8-529269fb1459",
        "_links": {
          "content": {
            "href": "https://dspace7-internal.atmire.com/rest/api/core/collections/8a085042-ba77-11e8-96f8-529269fb1459/exportToCsv/download/2018-09-17T09:24:24.0"
          },
          "self": {
            "href": "https://dspace7-internal.atmire.com/rest/api/core/collections/8a085042-ba77-11e8-96f8-529269fb1459/exportToCsv/view/2018-09-17T09:24:24.0"
          }
        }
      },
      {
        "date": "2018-09-17T09:24:28.000+0000",
        "state": "completed",
        "size": 6427,
        "type": "collections",
        "dso-id": "8a085042-ba77-11e8-96f8-529269fb1459",
        "_links": {
          "content": {
            "href": "https://dspace7-internal.atmire.com/rest/api/core/collections/8a085042-ba77-11e8-96f8-529269fb1459/exportToCsv/download/2018-09-17T09:24:28.0"
          },
          "self": {
            "href": "https://dspace7-internal.atmire.com/rest/api/core/collections/8a085042-ba77-11e8-96f8-529269fb1459/exportToCsv/view/2018-09-17T09:24:28.0"
          }
        }
      }
    ]
  }
}
```

It returns a list of all previously created csv files for the community/collection/item. This is similar to the zip export page

**/api/core/<:type>/<:uuid>/exportToCsv/create**

Example: <https://dspace7-internal.atmire.com/rest/#https://dspace7-internal.atmire.com/rest/api/core/community/8a085042-ba77-11e8-96f8-529269fb1459/exportToCsv/create>

It should start creating the csv file for the collection

The json representation is as & follow
```json
{
  "date": "2018-09-17T09:24:24.000+0000",
  "state": "In Progress",
  "type": "exportToCsv",
  "dso-id": "8a085042-ba77-11e8-96f8-529269fb1459",
  "_links": {
    "self": {
      "href": "https://dspace7-internal.atmire.com/rest/api/core/community/exportToCsv/40d6d1d8-bb11-11e8-96f8-529269fb1459/exportToCsv/view/2018-09-17T09:24:24.0"
    }
  }
}
```

[It creates a CSV file containing the items in the community/collection or from a single item. This is similar to http://demo.dspace.org/xmlui/csv/handle/10673/60, stores the csv file on the server, but doesn't return it nor waits until it's completed]

**/api/core/<:type>/<:uuid>/exportToCsv/view/<:date>**

Example: <https://dspace7-internal.atmire.com/rest/#https://dspace7-internal.atmire.com/rest/api/core/community/40d6d1d8-bb11-11e8-96f8-529269fb1459/exportToCsv/view/2018-09-10T09:37:24.0>

It should return the state of the csv export for the collection.
The state can be completed, in progress, not available.
The size is in bytes

The json representation is as follow
```json
{
  "date": "2018-09-17T09:24:28.000+0000",
  "state": "completed",
  "size": 427,
  "type": "exportToCsv",
  "dso-id": "8a085042-ba77-11e8-96f8-529269fb1459",
  "_links": {
    "content": {
      "href": "https://dspace7-internal.atmire.com/rest/api/core/item/exportToCsv/1cc86db0-bb11-11e8-96f8-529269fb1459/exportToCsv/download/2018-09-17T09:24:28.0"
    },
    "self": {
      "href": "https://dspace7-internal.atmire.com/rest/api/core/item/exportToCsv/1cc86db0-bb11-11e8-96f8-529269fb1459/exportToCsv/view/2018-09-17T09:24:28.0"
    }
  }
}
```

It view the state of a csv file containing the metadata of items in a community/collection or the metadata of a single item. This is similar to http://demo.dspace.org/xmlui/admin/export

**/api/core/<:type>/<:uuid>/exportToCsv/download/<:date>**

Example: <https://dspace7-internal.atmire.com/rest/#https://dspace7-internal.atmire.com/rest/api/core/item/1cc86db0-bb11-11e8-96f8-529269fb1459/exportToCsv/download/2018-09-10T09:37:24.0>

It should return the CSV file for the collection, assuming it's completed.

[It creates a CSV file containing the items in the community/collection or from a single item. This is similar to http://demo.dspace.org/xmlui/csv/handle/10673/46]