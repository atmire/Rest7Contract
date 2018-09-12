# Collection/Community/Item Export to ZIP Endpoint
[Back to the list of all defined endpoints](endpoints.md)

All the API requests below require admin permissions on the collection

**/api/core/<:type>/<:uuid>/exportToZip**

Example: <https://dspace7-internal.atmire.com/rest/#https://dspace7-internal.atmire.com/rest/api/core/collections/3b43a8bc-9f7c-499b-ac43-8e83519ec40c/exportToZip>

It should provide access to the list of exports for this collection.

The json representation is as follow
```json
{
  "type": "exportToZip",
  "_links": {
    "create": {
      "href": "https://dspace7-internal.atmire.com/rest/api/category/exportToZip/3b43a8bc-9f7c-499b-ac43-8e83519ec40c/exportToZip/create"
    },
    "self": {
      "href": "https://dspace7-internal.atmire.com/rest/api/core/collections/3b43a8bc-9f7c-499b-ac43-8e83519ec40c/exportToZip"
    }
  },
  "_embedded": {
    "exportToZip": [
      {
        "date": "2018-09-10T09:37:24.000+0000",
        "state": "completed",
        "size": 642783,
        "type": "collections",
        "dso-id": "3b43a8bc-9f7c-499b-ac43-8e83519ec40c",
        "_links": {
          "content": {
            "href": "https://dspace7-internal.atmire.com/rest/api/core/collections/3b43a8bc-9f7c-499b-ac43-8e83519ec40c/exportToZip/download/2018-09-10T09:37:24.0"
          },
          "self": {
            "href": "https://dspace7-internal.atmire.com/rest/api/core/collections/3b43a8bc-9f7c-499b-ac43-8e83519ec40c/exportToZip/view/2018-09-10T09:37:24.0"
          }
        }
      },
      {
        "date": "2018-09-10T09:37:28.000+0000",
        "state": "completed",
        "size": 642783,
        "type": "collections",
        "dso-id": "3b43a8bc-9f7c-499b-ac43-8e83519ec40c",
        "_links": {
          "content": {
            "href": "https://dspace7-internal.atmire.com/rest/api/core/collections/3b43a8bc-9f7c-499b-ac43-8e83519ec40c/exportToZip/download/2018-09-10T09:37:28.0"
          },
          "self": {
            "href": "https://dspace7-internal.atmire.com/rest/api/core/collections/3b43a8bc-9f7c-499b-ac43-8e83519ec40c/exportToZip/view/2018-09-10T09:37:28.0"
          }
        }
      }
    ]
  }
}
```

[It returns a list of all previously created ZIP files for the collection. This is similar to http://demo.dspace.org/xmlui/admin/export]

**/api/core/<:type>/<:uuid>/exportToZip/create**

Example: <https://dspace7-internal.atmire.com/rest/#https://dspace7-internal.atmire.com/rest/api/core/collections/3b43a8bc-9f7c-499b-ac43-8e83519ec40c/exportToZip/create>

It should start creating the ZIP file for the collection

The json representation is as follow
```json
{
  "date": "2018-09-12T12:34:54.000+0000",
  "state": "In Progress",
  "type": "exportToZip",
  "dso-id": "3b43a8bc-9f7c-499b-ac43-8e83519ec40c",
  "_links": {
    "self": {
      "href": "https://dspace7-internal.atmire.com/rest/api/category/exportToZip/3b43a8bc-9f7c-499b-ac43-8e83519ec40c/exportToZip/view/WedTSepT12T12:34:54TUTCT2018"
    }
  }
}
```

[It creates a ZIP file containing the SAF of each item in the collection. This is similar to http://demo.dspace.org/xmlui/admin/export?collectionID=99cb327a-e7ac-40ed-8540-03b86874149f, stores the ZIP file on the server, but doesn't return it nor waits until it's completed]

**/api/core/<:type>/<:uuid>/exportToZip/view/<:date>**

Example: <https://dspace7-internal.atmire.com/rest/#https://dspace7-internal.atmire.com/rest/api/core/collections/3b43a8bc-9f7c-499b-ac43-8e83519ec40c/exportToZip/view/2018-09-10T09:37:24.0>

It should return the state of the ZIP file for the collection.
The state can be completed, in progress, not available.
The size is in bytes

The json representation is as follow
```json
{
  "date": "2018-09-10T09:37:24.000+0000",
  "state": "completed",
  "size": 642783,
  "type": "exportToZip",
  "dso-id": "3b43a8bc-9f7c-499b-ac43-8e83519ec40c",
  "_links": {
    "content": {
      "href": "https://dspace7-internal.atmire.com/rest/api/category/exportToZip/3b43a8bc-9f7c-499b-ac43-8e83519ec40c/exportToZip/download/2018-09-10T09:37:24.0"
    },
    "self": {
      "href": "https://dspace7-internal.atmire.com/rest/api/category/exportToZip/3b43a8bc-9f7c-499b-ac43-8e83519ec40c/exportToZip/view/2018-09-10T09:37:24.0"
    }
  }
}
```

[It view the state of a ZIP file containing the SAF of each item in the collection. This is similar to http://demo.dspace.org/xmlui/admin/export]

**/api/core/<:type>/<:uuid>/exportToZip/download/<:date>**

Example: <https://dspace7-internal.atmire.com/rest/#https://dspace7-internal.atmire.com/rest/api/core/collections/3b43a8bc-9f7c-499b-ac43-8e83519ec40c/exportToZip/download/2018-09-10T09:37:24.0>

It should return the ZIP file for the collection, assuming it's completed.

[It returns a ZIP file containing the SAF of each item in the collection. This is similar to http://demo.dspace.org/xmlui/admin/export?collectionID=99cb327a-e7ac-40ed-8540-03b86874149f]
