# Item Type Endpoints
[Back to the list of all defined endpoints](endpoints.md)

This endpoint contains the various types of items (publication, person, journal, …)

## Main Endpoint
**/api/core/itemtypes**

A sample can be found at https://dspace7-entities.atmire.com/rest/#https://dspace7-entities.atmire.com/rest/api/core/itemtypes

```json
{
  "_embedded": {
    "itemtypes": [
      {
        "id": 1,
        "label": "Publication",
        "type": "itemtype",
        "_links": {
          "self": {
            "href": "https://dspace7-entities.atmire.com/rest/api/core/itemtypes/1"
          },
          "relationshiptypes": {
            "href": "https://dspace7-entities.atmire.com/rest/api/core/itemtypes/1/relationshiptypes"
          }
        }
      },
      {
        "id": 2,
        "label": "Person",
        "type": "itemtype",
        "_links": {
          "self": {
            "href": "https://dspace7-entities.atmire.com/rest/api/core/itemtypes/2"
          },
          "relationshiptypes": {
            "href": "https://dspace7-entities.atmire.com/rest/api/core/itemtypes/2/relationshiptypes"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://dspace7-entities.atmire.com/rest/api/core/itemtypes"
    }
  },
  "page": {
    "size": 20,
    "totalElements": 2,
    "totalPages": 1,
    "number": 0
  }
}
```

## Single Item Type
**/api/core/itemtypes/<:id>**

A sample can be found at https://dspace7-entities.atmire.com/rest/#https://dspace7-entities.atmire.com/rest/api/core/itemtypes/1

```json
{
  "id": 1,
  "label": "Publication",
  "type": "itemtype",
  "_links": {
    "self": {
      "href": "https://dspace7-entities.atmire.com/rest/api/core/itemtypes/1"
    },
    "relationshiptypes": {
      "href": "https://dspace7-entities.atmire.com/rest/api/core/itemtypes/1/relationshiptypes"
    }
  }
}
```

It contains a HAL link to the Relationship Types for the current Item Type (not embedded)

## Relationship Types for the current Item Type
**/api/core/itemtypes/<:id>/relationshiptypes**

A sample can be found at https://dspace7-entities.atmire.com/rest/#https://dspace7-entities.atmire.com/rest/api/core/itemtypes/1/relationshiptypes
It embeds the [relationshiptypes](relationshiptypes.md) which are linked to the given item type (either on the left or right side)
