# Relationship Endpoints
[Back to the list of all defined endpoints](endpoints.md)

This endpoint contains the actual relationships connecting 2 items.
It uses a [relationship type](relationshiptypes.md) and the 2 items with HAL links

## Main Endpoint
**/api/core/relationships**

A sample can be found at https://dspace7-entities.atmire.com/rest/#https://dspace7-entities.atmire.com/rest/api/core/relationshiptypes

## Single Relationship
**/api/core/relationships/<:id>**

A sample can be found at https://dspace7-entities.atmire.com/rest/#https://dspace7-entities.atmire.com/rest/api/core/relationships/530
The leftId and rightId parameter in JSON may still be present, but they will be removed soon (requires other PRs to be merged first)

```json
{
  "id": 530,
  "relationshipTypeId": 0,
  "leftPlace": 1,
  "rightPlace": 1,
  "type": "relationship",
  "_links": {
    "relationshipType": {
      "href": "https://dspace7-entities.atmire.com/rest/api/core/relationshiptypes/1"
    },
    "self": {
      "href": "https://dspace7-entities.atmire.com/rest/api/core/relationships/530"
    },
    "leftItem": {
      "href": "https://dspace7-entities.atmire.com/rest/api/core/items/e98b0f27-5c19-49a0-960d-eb6ad5287067"
    },
    "rightItem": {
      "href": "https://dspace7-entities.atmire.com/rest/api/core/items/0ffbee3f-e7ea-42bc-92fe-2fbef1a52c0f"
    }
  },
  "_embedded": {
    "relationshipType": {
      "id": 1,
      "leftLabel": "isAuthorOfPublication",
      "rightLabel": "isPublicationOfAuthor",
      "leftMinCardinality": 5,
      "leftMaxCardinality": 2147483647,
      "rightMinCardinality": 0,
      "rightMaxCardinality": 20000,
      "type": "relationshiptype",
      "_links": {
        "leftType": {
          "href": "https://dspace7-entities.atmire.com/rest/api/core/entitytypes/1"
        },
        "rightType": {
          "href": "https://dspace7-entities.atmire.com/rest/api/core/entitytypes/2"
        },
        "self": {
          "href": "https://dspace7-entities.atmire.com/rest/api/core/relationshiptypes/1"
        }
      },
      "_embedded": {
        "leftType": {
          "id": 1,
          "label": "Publication",
          "type": "entitytype",
          "_links": {
            "self": {
              "href": "https://dspace7-entities.atmire.com/rest/api/core/entitytypes/1"
            },
            "relationshiptypes": {
              "href": "https://dspace7-entities.atmire.com/rest/api/core/entitytypes/1/relationshiptypes"
            }
          }
        },
        "rightType": {
          "id": 2,
          "label": "Person",
          "type": "entitytype",
          "_links": {
            "self": {
              "href": "https://dspace7-entities.atmire.com/rest/api/core/entitytypes/2"
            },
            "relationshiptypes": {
              "href": "https://dspace7-entities.atmire.com/rest/api/core/entitytypes/2/relationshiptypes"
            }
          }
        }
      }
    }
  }
}
```

The [relationship type](relationshiptypes.md) is embedded
The 2 items are included as HAL links but are not embedded

## Creating a relationship

**POST /api/core/relationships?leftItem=<:itemuuid>&rightItem=<:itemuuid>&relationshipType=<:relationshipType>**

A new relationship between 2 items can be created by specifying both items and the relationshipType

A sample CURL command would be:
```
curl -D - -X POST 'https://dspace7-entities.atmire.com/rest/api/core/relationships?leftItem=12623672-25a9-4df2-ab36-699c4c240c7e&rightItem=5a3f7c7a-d3df-419c-8a2-f00ede62c60a&relationshipType=1' -H 'Authorization: Bearer eyJhbGciO…' -H "content-type: application/json"  --data '{}'
```

No JSON data is required since all information is included in the 3 parameters

## Updating a relationship

**PUT /api/core/relationships/<:id>?leftItem=<:itemuuid>&rightItem=<:itemuuid>&relationshipType=<:relationshipType>**

Update the parameters in the relationship (e.g. changing the item)

A sample CURL command would be:
```
curl -D - -X PUT 'https://dspace7-entities.atmire.com/rest/api/core/relationships/891?leftItem=12623672-25a9-4df2-ab36-699c4c240c7e&rightItem=5a3f7c7a-d3df-419c-8a2-f00ede62c60a&relationshipType=1' -H 'Authorization: Bearer eyJhbGciO…' -H "content-type: application/json"  --data '{}'
```

No JSON data is required since all information is included in the 3 parameters

## Relationships per item
**/api/core/items/<:uuid>/relationships**

A sample can be found at https://dspace7-entities.atmire.com/rest/#https://dspace7-entities.atmire.com/rest/api/core/items/5a3f7c7a-d3df-419c-b8a2-f00ede62c60a/relationships

It embeds all relationships where either the left or the right item matches the given uuid

## Relationships per Relationship type
**/api/core/relationships/<:relationshipname>**

A sample can be found at https://dspace7-entities.atmire.com/rest/#https://dspace7-entities.atmire.com/rest/api/core/relationships/isPersonOfOrgUnit

This is similar to
https://dspace7-entities.atmire.com/rest/#https://dspace7-entities.atmire.com/rest/api/discover/facets/author

It embeds all relationships where the relationship type has the given name on either the left or the right label


This can be filtered to a single DSO using https://dspace7-entities.atmire.com/rest/#https://dspace7-entities.atmire.com/rest/api/core/relationships/isPersonOfOrgUnit?dso=f2235aa6-6fe7-4174-a690-598b72dd8e44 which contains all relationships created using the relationship type isPersonOfOrgUnit for which one item is f2235aa6-6fe7-4174-a690-598b72dd8e44

This is similar to https://dspace7-entities.atmire.com/rest/#https://dspace7-entities.atmire.com/rest/api/discover/facets/author?query=test

## Deleting a relationship

**DELETE /api/core/relationships/<:id>**

Delete a relationship between 2 items.

A sample CURL command would be:
```
curl -D - -XDELETE 'https://dspace7-entities.atmire.com/rest/api/core/relationships/890'  -H 'Authorization: Bearer eyJhbGciO…'
```

* 204 No content - if the operation succeed
* 401 Forbidden - if you are not authenticated
* 403 Unauthorized - if you are not logged in with sufficient permissions
* 404 Not found - if the item doesn't exist (or was already deleted)
