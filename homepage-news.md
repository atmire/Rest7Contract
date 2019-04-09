# Homepage News Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**/api/config/pages**   

Provide access to the list of all static pages (currently home page news only). These are pages not specific to any items. The design of the REST contract should allow it to be extended to e.g. images as well.
Because the XMLUI supports home page news per language, multiple pages can be created here.

Example:
```json
{
  "_embedded": {
    "pages": [
      {
        "id": "004a297e-fd06-4662-ae51-73e4b7c165c8",
        "name": "home-page-news",
        "title": "DSpace Demo Repository",
        "sizeBytes": 234,
        "language": "en",
        "type": "page",
        "_links": {
          "content": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/004a297e-fd06-4662-ae51-73e4b7c165c8/content"
          },
          "format": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/004a297e-fd06-4662-ae51-73e4b7c165c8/format"
          },
          "self": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/004a297e-fd06-4662-ae51-73e4b7c165c8"
          }
        },
        "_embedded": {
          "format": {
            "id": 22,
            "shortDescription": "XHTML",
            "description": "XHTML",
            "mimetype": "text/html; charset=utf-8",
            "supportLevel": 0,
            "internal": false,
            "extensions": null,
            "type": "bitstreamformat",
            "_links": {
              "self": {
                "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/bitstreamformats/22"
              }
            }
          }
        }
      },
    ]
  }
}
```

## Single page
### View page
**/api/config/pages/<:uuid>**

Provide detailed information about a static page. The JSON response document is as follow
```json
{
  "id": "004a297e-fd06-4662-ae51-73e4b7c165c8",
  "name": "home-page-news",
  "title": "DSpace Demo Repository",
  "sizeBytes": 234,
  "language": "en",
  "type": "page"
}
```

Exposed links:
* format: link to the format resource associated with the file (XHTML, jpeg, etc.). TODO: verify how images can be supported
* content: link to access the actual content of the page

### Edit page: Multipart POST Method
**POST /api/config/pages**

A multipart POST request will result in creating a new file identified by the name.

Send detailed information about a static page, and the actual file. The sizeBytes and uuid is not required, but the other attributes are applicable

**PUT /api/config/pages/<:uuid>**

A multipart PUT request will result in an update of the file identified by the uuid.

Send detailed information about a static page, and the actual file. The sizeBytes is not required, but the other attributes are applicable

### Delete page
**DELETE /api/config/pages/<:uuid>**

A DELETE request will typically result in deleting the file identified by the uuid. If the file didn't exist yet, the delete will fail

## Linked entities
### Format
**/api/config/pages/<:uuid>/format**

Example: Similar to bitstreams

It returns the format of the resource

### Content
**/api/config/pages/<:uuid>/content**

Example: Similar to bitstreams

It returns the actual content (bits) of the resource

Response Headers:

* **Content-Type**: the mimetype as recorded for the file
* **Content-Length**: the size in bytes of the content

The supported **Request Headers** are:
* If-Modified-Since: 
* If-None-Match: 

### Languages
**/api/config/pages/search/languages?name=<:page-name>**

Example:
```json
{
  "_embedded": {
    "pages": [
      {
        "id": "004a297e-fd06-4662-ae51-73e4b7c165c8",
        "name": "home-page-news",
        "title": "DSpace Demo Repository",
        "sizeBytes": 234,
        "language": "en",
        "type": "page",
        "_links": {
          "content": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/004a297e-fd06-4662-ae51-73e4b7c165c8/content"
          },
          "format": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/004a297e-fd06-4662-ae51-73e4b7c165c8/format"
          },
          "self": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/004a297e-fd06-4662-ae51-73e4b7c165c8"
          }
        },
        "_embedded": {
          "format": {
            "id": 22,
            "shortDescription": "XHTML",
            "description": "XHTML",
            "mimetype": "text/html; charset=utf-8",
            "supportLevel": 0,
            "internal": false,
            "extensions": null,
            "type": "bitstreamformat",
            "_links": {
              "self": {
                "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/bitstreamformats/22"
              }
            }
          }
        }
      },
      {
        "id": "1054a711-b307-4052-af28-4162d36d2eca",
        "name": "home-page-news",
        "title": "DSpace Démo Dépôt",
        "language": "fr",
        "sizeBytes": 0,
        "type": "page",
        "_links": {
          "content": {
            "href": "https://dspace7-internal.atmire.com/rest/api/config/pages/1054a711-b307-4052-af28-4162d36d2eca/content"
          },
          "format": {
            "href": "https://dspace7-internal.atmire.com/rest/api/config/pages/1054a711-b307-4052-af28-4162d36d2eca/format"
          },
          "self": {
            "href": "https://dspace7-internal.atmire.com/rest/api/config/pages/1054a711-b307-4052-af28-4162d36d2eca"
          }
        },
        "_embedded": {
          "format": null
        }
      }
    ],
    "_links": {
      "self": {
        "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/search/languages"
      }
    }
  }
}
```

It returns all the language variants of the resource
