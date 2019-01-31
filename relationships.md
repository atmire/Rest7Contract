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
      "leftMinCardinality": 0,
      "leftMaxCardinality": null,
      "rightMinCardinality": 0,
      "rightMaxCardinality": null,
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

**POST /api/core/relationships?relationshipType=<:relationshipType>**

A new relationship between 2 items can be created by specifying both items in a uri-list body and specifying the relationshipType as a parameter

A sample CURL command would be:
```
curl -i -X POST 'https://dspace7-entities.atmire.com/rest/api/core/relationships?relationshipType=1' -H 'Authorization: Bearer eyJhbGciO…' -H "Content-Type:text/uri-list" --data 'https://dspace7-entities.atmire.com/rest/api/core/items/12623672-25a9-4df2-ab36-699c4c240c7e \n https://dspace7-entities.atmire.com/rest/api/core/items/5a3f7c7a-d3df-419c-8a2-f00ede62c60a'
```

The uri-list should always contain exactly 2 items. The first item will be used as the left Item. The second item will be used as the right Item.
The relationshipType parameter is mandatory as well

## Updating a relationship

**PUT /api/core/relationships/<:id>**

Update the items in the relationship

A sample CURL command would be:
```
curl -i -X PUT 'https://dspace7-entities.atmire.com/rest/api/core/relationships/891' -H 'Authorization: Bearer eyJhbGciO…' -H "Content-Type:text/uri-list" --data 'https://dspace7-entities.atmire.com/rest/api/core/items/12623672-25a9-4df2-ab36-699c4c240c7e \n https://dspace7-entities.atmire.com/rest/api/core/items/5a3f7c7a-d3df-419c-8a2-f00ede62c60a'
```

The uri-list should always contain exactly 2 items. The first item will be used as the left Item. The second item will be used as the right Item.
The relationshipType is not modifiable

## Relationships per Relationship type
**/api/core/relationships/search/byLabel?label=<:relationshipname>**

A sample search would be https://dspace7-entities.atmire.com/rest/#https://dspace7-entities.atmire.com/rest/api/core/relationships/search/byLabel?label=isPersonOfOrgUnit
The relationshipname parameter is mandatory

It would respond with
```json
{
  "_embedded": {
    "relationships": [
      {
        "id": 590,
        "leftId": "f2235aa6-6fe7-4174-a690-598b72dd8e44",
        "relationshipTypeId": 0,
        "rightId": "d30de96b-1e76-40ae-8ef9-ab426b6f9763",
        "leftPlace": 1,
        "rightPlace": 2,
        "type": "relationship",
        "_links": {
          "relationshipType": {
            "href": "https://dspace7-entities.atmire.com/rest/api/core/relationshiptypes/5"
          },
          "self": {
            "href": "https://dspace7-entities.atmire.com/rest/api/core/relationships/590"
          },
          "leftItem": {
            "href": "https://dspace7-entities.atmire.com/rest/api/core/items/f2235aa6-6fe7-4174-a690-598b72dd8e44"
          },
          "rightItem": {
            "href": "https://dspace7-entities.atmire.com/rest/api/core/items/d30de96b-1e76-40ae-8ef9-ab426b6f9763"
          }
        },
        "_embedded": {
          "relationshipType": {
            "id": 5,
            "leftLabel": "isOrgUnitOfPerson",
            "rightLabel": "isPersonOfOrgUnit",
            "leftMinCardinality": 0,
            "leftMaxCardinality": null,
            "rightMinCardinality": 0,
            "rightMaxCardinality": null,
            "type": "relationshiptype",
            "_links": {
              "leftType": {
                "href": "https://dspace7-entities.atmire.com/rest/api/core/entitytypes/2"
              },
              "rightType": {
                "href": "https://dspace7-entities.atmire.com/rest/api/core/entitytypes/4"
              },
              "self": {
                "href": "https://dspace7-entities.atmire.com/rest/api/core/relationshiptypes/5"
              }
            },
            "_embedded": {
              "leftType": {
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
              },
              "rightType": {
                "id": 4,
                "label": "OrgUnit",
                "type": "entitytype",
                "_links": {
                  "self": {
                    "href": "https://dspace7-entities.atmire.com/rest/api/core/entitytypes/4"
                  },
                  "relationshiptypes": {
                    "href": "https://dspace7-entities.atmire.com/rest/api/core/entitytypes/4/relationshiptypes"
                  }
                }
              }
            }
          }
        }
      },
      {
        "id": 589,
        "leftId": "5a3f7c7a-d3df-419c-b8a2-f00ede62c60a",
        "relationshipTypeId": 0,
        "rightId": "c216201f-ed10-4361-b0e0-5a065405bd3e",
        "leftPlace": 2,
        "rightPlace": 1,
        "type": "relationship",
        "_links": {
          "relationshipType": {
            "href": "https://dspace7-entities.atmire.com/rest/api/core/relationshiptypes/5"
          },
          "self": {
            "href": "https://dspace7-entities.atmire.com/rest/api/core/relationships/589"
          },
          "leftItem": {
            "href": "https://dspace7-entities.atmire.com/rest/api/core/items/5a3f7c7a-d3df-419c-b8a2-f00ede62c60a"
          },
          "rightItem": {
            "href": "https://dspace7-entities.atmire.com/rest/api/core/items/c216201f-ed10-4361-b0e0-5a065405bd3e"
          }
        },
        "_embedded": {
          "relationshipType": {
            "id": 5,
            "leftLabel": "isOrgUnitOfPerson",
            "rightLabel": "isPersonOfOrgUnit",
            "leftMinCardinality": 0,
            "leftMaxCardinality": null,
            "rightMinCardinality": 0,
            "rightMaxCardinality": null,
            "type": "relationshiptype",
            "_links": {
              "leftType": {
                "href": "https://dspace7-entities.atmire.com/rest/api/core/entitytypes/2"
              },
              "rightType": {
                "href": "https://dspace7-entities.atmire.com/rest/api/core/entitytypes/4"
              },
              "self": {
                "href": "https://dspace7-entities.atmire.com/rest/api/core/relationshiptypes/5"
              }
            },
            "_embedded": {
              "leftType": {
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
              },
              "rightType": {
                "id": 4,
                "label": "OrgUnit",
                "type": "entitytype",
                "_links": {
                  "self": {
                    "href": "https://dspace7-entities.atmire.com/rest/api/core/entitytypes/4"
                  },
                  "relationshiptypes": {
                    "href": "https://dspace7-entities.atmire.com/rest/api/core/entitytypes/4/relationshiptypes"
                  }
                }
              }
            }
          }
        }
      },
      …
    ]
  },
  "_links": {
    "self": {
      "href": "https://dspace7-entities.atmire.com/rest/api/core/relationships/search/byLabel?label=isPersonOfOrgUnit"
    }
  },
  "page": {
    "number": 0,
    "size": 20,
    "totalPages": 1,
    "totalElements": 2
  }
}
```

This is similar to
https://dspace7-internal.atmire.com/rest/#/rest/api/core/communities/search/subCommunities?parent=daa2657d-5f39-4876-9536-ace42e96b440

It embeds all relationships where the relationship type has the given label on either the left or the right label


This can be further filtered to a single DSO using 
https://dspace7-entities.atmire.com/rest/#https://dspace7-entities.atmire.com/rest/api/core/relationships/search/byLabel?label=isPersonOfOrgUnit&dso=f2235aa6-6fe7-4174-a690-598b72dd8e44 which contains all relationships created using the relationship type isPersonOfOrgUnit for which one item is f2235aa6-6fe7-4174-a690-598b72dd8e44
The dso parameter is optional

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
