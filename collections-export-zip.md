# Collection Export to ZIP Endpoint
[Back to the list of all defined endpoints](endpoints.md)

All the API requests below require admin permissions on the collection

**/api/core/collections/<:uuid>/exportToZip**

Example: <https://dspace7.4science.it/dspace-spring-rest/#https://dspace7.4science.it/dspace-spring-rest/api/core/collections/1c11f3f1-ba1f-4f36-908a-3f1ea9a557eb/exportToZip>

It should provide access to the list of exports for this collection.

The json representation is as follow
```json
{
  "_embedded": {
    "exportToZip": [
      {
        "collection-id": "1c11f3f1-ba1f-4f36-908a-3f1ea9a557eb",
        "date": "2018-07-23T13:20:29",
        "_links": {
          "self": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/collections/1c11f3f1-ba1f-4f36-908a-3f1ea9a557eb/exportToZip/view/2018-07-23T13:20:29"
          }
        }
      },
      {
        "collection-id": "1c11f3f1-ba1f-4f36-908a-3f1ea9a557eb",
        "date": "2018-07-26T09:33:08",
        "_links": {
          "self": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/collections/1c11f3f1-ba1f-4f36-908a-3f1ea9a557eb/exportToZip/view/2018-07-26T09:33:08"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/collections/1c11f3f1-ba1f-4f36-908a-3f1ea9a557eb/exportToZip"
    }
  }
}
```

[It returns a list of all previously created ZIP files for the collection. This is similar to http://demo.dspace.org/xmlui/admin/export]

**/api/core/collections/<:uuid>/exportToZip/create**

Example: <https://dspace7.4science.it/dspace-spring-rest/#https://dspace7.4science.it/dspace-spring-rest/api/core/collections/1c11f3f1-ba1f-4f36-908a-3f1ea9a557eb/exportToZip/create>

It should start creating the ZIP file for the collection

The json representation is as follow
```json
{
  "collection-id": "1c11f3f1-ba1f-4f36-908a-3f1ea9a557eb",
  "date": "2018-07-26T09:38:13",
  "_links": {
    "self": {
      "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/collections/1c11f3f1-ba1f-4f36-908a-3f1ea9a557eb/exportToZip/view/2018-07-26T09:38:13"
    }
}
```

[It creates a ZIP file containing the SAF of each item in the collection. This is similar to http://demo.dspace.org/xmlui/admin/export?collectionID=99cb327a-e7ac-40ed-8540-03b86874149f, stores the ZIP file on the server, but doesn't return it nor waits until it's completed]

**/api/core/collections/<:uuid>/exportToZip/view/<:date>**

Example: <https://dspace7.4science.it/dspace-spring-rest/#https://dspace7.4science.it/dspace-spring-rest/api/core/collections/1c11f3f1-ba1f-4f36-908a-3f1ea9a557eb/exportToZip/view/2018-07-26T09:38:13>

It should return the state of the ZIP file for the collection.
The state can be completed, in progress, not available.
The size is in bytes

The json representation is as follow
```json
{
  "collection-id": "1c11f3f1-ba1f-4f36-908a-3f1ea9a557eb",
  "date": "2018-07-26T09:38:13",
  "state": "completed",
  "size": "2456231",
  "_links": {
    "self": {
      "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/collections/1c11f3f1-ba1f-4f36-908a-3f1ea9a557eb/exportToZip/view/2018-07-26T09:38:13"
    }
}
```

[It view the state of a ZIP file containing the SAF of each item in the collection. This is similar to http://demo.dspace.org/xmlui/admin/export]

**/api/core/collections/<:uuid>/exportToZip/download/<:date>**

Example: <https://dspace7.4science.it/dspace-spring-rest/#https://dspace7.4science.it/dspace-spring-rest/api/core/collections/1c11f3f1-ba1f-4f36-908a-3f1ea9a557eb/exportToZip/download/2018-07-26T09:38:13>

It should return the ZIP file for the collection, assuming it's completed.

[It returns a ZIP file containing the SAF of each item in the collection. This is similar to http://demo.dspace.org/xmlui/admin/export?collectionID=99cb327a-e7ac-40ed-8540-03b86874149f]
