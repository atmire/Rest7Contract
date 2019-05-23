# Versioning endpoints

[Back to the list of all defined endpoints](endpoints.md)

## Create version

**POST /api/versioning/version?item=<:itemUUID>**

To create a new version for an item, perform as post with the JSON below when logged in as admin.

```
{
    "summary": "The reason for creating a version",
    "type": "version"
}
```

* 200 OK - if the operation succeed
* 400 Bad Request - if the summary if empty 
* 403 Unauthorized - if you are not logged in as an administrator
* 404 Not found - if the item doesn't exist
* 422 Unprocessable Entity 
    - If the provided item latest version isn't archived yet 
    - If the provided item isn't archived
    - If the item was harvested from an OAI source
    
When a version is created the version is returned, see below in the "GET /api/versioning/version/<:versionId>" for the response.

## Get version history

**GET /api/versioning/versionHistory/<:versionHistoryId>**

Provide version information for the version history id.

```
{
  "id": "1",
  "type": "versionHistory",
  "_links": {
    "self": {
      "href": "https://dspace7.4science.it/dspace-spring-rest/api/versioning/versionHistory/1"
    },
    "versions": {
      "href": "https://dspace7.4science.it/dspace-spring-rest/api/versioning/versionHistory/1/versions"
    }
  },
  "_embedded": {
    "versions": [
      {
        "id": "101",
        "version": "1",
        "type": "version",
        ...
      },
      {
        "id": "101",
        "version": "1",
        "type": "version",
        ...
      }
    ]
  }
}
```

**GET /api/versioning/versionHistory/<:versionHistoryId>/versions**

Retrieve all the versions for the provided version history identifier.

```
{
  "_embedded": {
    "versions": [
      {
        "id": "101",
        "version": "1",
        "type": "version",
        ...
      },
      {
        "id": "101",
        "version": "1",
        "type": "version",
        ...
      }
    ]
  }
}
```

## Get single version

**GET /api/versioning/version/<:versionId>**

Provide version information for the version id.

```
{
  "id": "101",
  "version": "2",
  "type": "version",
  "created": "2015-11-03T09:44:46.617",
  "Summary": "Fixing some typos in the abstract",
  "_links": {
    "versionHistory": {
      "href": "https://dspace7.4science.it/dspace-spring-rest/api/versioning/versionHistory/10"
    },
    "self": {
      "href": "https://dspace7.4science.it/dspace-spring-rest/api/versioning/version/101"
    },
    "submitter": {
      "href": "https://dspace7.4science.it/dspace-spring-rest/api/eperson/epersons/91b335e7-7bd6-4726-96ac-cf05794aba79"
    },
    "item": {
      "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/items/b0ae9093-d771-4b12-80de-f356f3b0d067"
    }
  },
  "_embedded": {
    "submitter": {
      "id": "a6086b34-3918-45b7-8ddd-9329a702a26a",
      "uuid": "a6086b34-3918-45b7-8ddd-9329a702a26a",
      "name": "dspace@dspace.org",
      "handle": null
    },
    "item": {
      "id": "b0ae9093-d771-4b12-80de-f356f3b0d067",
      "uuid": "b0ae9093-d771-4b12-80de-f356f3b0d067",
      "name": "Test item"
    }
  }
}
```


**GET /api/versioning/item/<:itemId>**

Provide version information for the item id.

The JSON response is the same as the endpoint above.


## Remove version

**DELETE /api/versioning/version/<:versionId>**

Delete a version

* 204 No content - if the operation succeed
* 403 Unauthorized - if you are not logged in as an administrator
* 404 Not found - if the version doesn't exist

## Update version

**PUT /api/versioning/version/<:versionId>**

Provide updated summary for a certain version when logged in as admin

```
{
    "summary": "Updated reason",
    "type": "version"
}
```

* 204 No content - if the operation succeed
* 400 Bad Request - if the summary if empty 
* 403 Unauthorized - if you are not logged in as an administrator
* 404 Not found - if the version doesn't exist